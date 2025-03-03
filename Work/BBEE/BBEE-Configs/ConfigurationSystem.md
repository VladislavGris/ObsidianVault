## Основные положения

- Отправка настроек идет раз в секунду (1 Hz)
- Настройки блоков сохраняются на АРМ-К
- Приложение должно стартовать в фоне без UI, чтобы при перезапуске выдать настройки блокам
- Для отправки настроек на устройства создается отдельный демон, который читает настройки каждую секунду и отправляет
- UI только записывает настройки в файлы
- UI должен быть крупным
- После запуска программы появляются крупные кнопки для открытия настройки блоков
- По нажатию кнопки для блока открывается приложение/отдельное окно виджета (диалог)
- Основной приоритет - литеры, юстировка, бинс

## Ссылки на репозитории с протоколами

- https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/LanKsa/SynthManagement.h?at=refs%2Fheads%2FsynthControl
- https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/LanSscSvrSrp/VsoAdjustment.h?at=refs%2Fheads%2Ffeat%2Fsettings
- https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/LanKsa/RxSystemParam.h?at=refs%2Fheads%2Ffeat%2Fsettings

## Описание

Программа работы с настройками блоков.
Предоставляет GUI для установки настроек.
Настройки каждого блока реализуются в отдельном диалоге.

Точкой входа является `BlockSelectionController.cpp`. В его конструкторе создаются интерфейсы для остальных блоков и добавляются кнопки для их открытия на главное окно. Пример добавления интерфейса для `SynthSettings`:

```cpp
BlockSelectionController::BlockSelectionController(const QString configDirPath, ConfigurationSystem::BlockSelectionView *view) :
    QObject(),
    _view(view)
{
    auto synthView  = new ConfigurationSystem::SynthSettingsView(_view);
    auto synthController = std::make_unique<ConfigurationSystem::SynthSettingsController>(synthView, std::make_unique<SynthSettingsModel>(configDirPath));
    _view->AddBlock("Synth", synthView);
    _blockControllers.push_back(std::move(synthController));
}
```

## Добавление нового UI настроек

Для реализации нового UI нужно определить 3 новых класса:
- Model - содержит данные настроек и методы для работы с ними
- View - представляет GUI для работы с настройками и обновляет данные модели при изменении UI
- Controller - связующее звено между Model и View, осуществляет коммуникацию между ними

### Создание класса Model

- Унаследовать созданный класс от `IBlockSettingsModel`
- Добавить в качестве члена класса структуру, которой соответствует сохраненный файл настроек, и геттер функцию для получения ссылки на эту структуру:

```cpp
#pragma once
#include "IBlockSettingsModel.h"
#include <BBEE-AWC-ConfigurationLib/src/Data/SynthSettingsData.h>

namespace ConfigurationSystem
{
    class SynthSettingsModel : public IBlockSettingsModel
    {
    public:
        SynthSettingsModel(const QString configDirPath);
		// Геттер
        Configuration::Data::SynthSettingsData& GetSettingsData();

    private:
	    // Структура с настройками
        Configuration::Data::SynthSettingsData _currentSettingsData {};
    };
}

```

- В конструкторе создать для базового класса экземпляр класса, унаследованного от `SettingsInterface` из [BBEE-AWC-ConfigurationLib](https://repo.okbtsp.com/projects/BBEEAWC/repos/bbee-awc-configuationlib/browse), который осществляет чтение/запись настроек в структуру класса:

```cpp
#include "SynthSettingsModel.h"
#include <BBEE-AWC-ConfigurationLib/src/SynthSettings.h>

using ConfigurationSystem::SynthSettingsModel;

SynthSettingsModel::SynthSettingsModel(const QString configDirPath) :
    IBlockSettingsModel(std::make_unique<Configuration::SynthSettings>(configDirPath + "SynthSettings.set", &_currentSettingsData)) { }

Configuration::Data::SynthSettingsData &SynthSettingsModel::GetSettingsData()
{
    return _currentSettingsData;
}
```

### Создание класса View

- Унаследовать класс от `IBlockSettingsView`. Переданный в конструкторе *parent* должен быть главным окном для унаследования от него стилей
- В конструкторе настраиваем UI в зависимости от нужд интерфейса и добавляем 2 коннекта для кнопок *OK* и *Cancel*:

```cpp
SynthSettingsView::SynthSettingsView(QWidget *parent) :
    IBlockSettingsView(parent),
    _ui(new Ui::SynthSettingsView())
{
    _ui->setupUi(this);

    _ui->modePilotSyntComboBox->addItem("ССЦ");
    _ui->modePilotSyntComboBox->addItem("СВР");

    connect(_ui->applyButtonBox, &QDialogButtonBox::accepted, this, &IBlockSettingsView::OnAcceptButtonPressed);
    connect(_ui->applyButtonBox, &QDialogButtonBox::rejected, this, &IBlockSettingsView::OnRejectButtonPressed);
}
```

- Определяем функцию `SetupDataTriggers`, принимающую в качестве параметра ссылку на структуру с настройками. В функции реализуем маппинг элементов UI на поля структуры, которые они должны обновлять:

```cpp
void SynthSettingsView::SetupDataTriggers(SynthSettingsData& settings)
{
    AddUpdater(CHECKBOX(_ui->hzErrResetCheckBox, settings.hzManagement.pgn339_Bsch1_6GHzManage, errReset));

    AddUpdater(CHECKBOX(_ui->synthSocErrResetCheckBox, settings.synthManagement.pgn30B_SynthesizerSocManage, errReset));

    AddUpdater(SPINBOX(_ui->bgzSocLiteraSpinBox, settings.bzgSocManagement.pgn308_BzgSocManage, litera));
    AddUpdater(CHECKBOX(_ui->bzgSocPilotSyntEnCheckBox, settings.bzgSocManagement.pgn308_BzgSocManage, pilotSyntEn));
    AddUpdater(CHECKBOX(_ui->bzgSocErrResetCheckBox, settings.bzgSocManagement.pgn308_BzgSocManage, errReset));

    AddUpdater(SPINBOX(_ui->literaSscSpinBox, settings.bzgSscSvrManagement.pgn30A_BzgSscSvrManage, literaSsc));
    AddUpdater(SPINBOX(_ui->literaSvrSpinBox, settings.bzgSscSvrManagement.pgn30A_BzgSscSvrManage, literaSvr));
    AddUpdater(CHECKBOX(_ui->bzgSscSvrPilotSyntEnCheckBox, settings.bzgSscSvrManagement.pgn30A_BzgSscSvrManage, pilotSyntEn));
    AddUpdater(COMBOBOX(_ui->modePilotSyntComboBox, settings.bzgSscSvrManagement.pgn30A_BzgSscSvrManage, modePilotSynt));
    AddUpdater(CHECKBOX(_ui->bzgSscSverErrResetCheckBox, settings.bzgSscSvrManagement.pgn30A_BzgSscSvrManage, errReset));
}

```

- `CHECKBOX`, `SPINBOX` и `COMBOBOX` это макросы, определенные в классах, унаследованных от `IUiUpdater`. Они создают унаследованные от класса `IUiUpdater` экземпляры апдейтеров, соответствующие названию. Параметры:
	1) Указатель на элемент управления UI
	2) Путь к структуре с настройками
	3) Имя поля в этой структуре
- После описания интерфейса таким образом поля структуры будут автоматически обновлятся при изменении значения на UI, а также UI будет обновляться в соответствии со значениями структуры, считанными при открытии диалога из файла настроек

### Создание класса Controller

- Унаследовать класс от `IBlockSettingsController`, передать в конструктор базового класса: 
	- Указатель на View (передается обычный указатель и не удаляется, т.к. предполагается, что управлять им будет переданный в конструктор *parent*, т.е. главное окно)
	- `unique_ptr` на Model, при этом вызывается `std::move` для передачи во владение
- Вызвать в конструкторе метод `SetupDataTriggers` у View и передать в качестве параметра значение, полученное из функции `GetSettingsData` у Model маппинга параметров настроек на UI:

```cpp
#include "SynthSettingsController.h"
#include "SynthSettingsModel.h"
#include "SynthSettingsView.h"

ConfigurationSystem::SynthSettingsController::SynthSettingsController(SynthSettingsView *view, std::unique_ptr<SynthSettingsModel> model) :
    IBlockSettingsController(view, std::move(model))
{
    dynamic_cast<SynthSettingsView*>(_view)->SetupDataTriggers(dynamic_cast<SynthSettingsModel*>(_model.get())->GetSettingsData());
}
```

## EnumeratedSettingsView

Если имеется структура с полем, явзяющимся `enum` зачением, указывающим тип структуры, то для реализации View нужно использовать `EnumeratedSettingsView`.

`EnumeratedSettingsView` сразу предоставляет .ui форму, на которой расположены QComboBox для выбора типа, QStackedWidget, на который добавляются виджеты с параметрами структуры, и QButtonBox с кнопками "ОК" и "Cancel".

Для реализации унаследованного от него класса необходимо:

- Определить в конструкторе типы, добавлением из в QComboBox:

```cpp
VsoSettingsView::VsoSettingsView(QWidget *parent) :
    EnumeratedSettingsView(parent)
{
    AddEnumComboBoxItem("ССЦ");
    AddEnumComboBoxItem("СВР 1 Захват (Широкий луч)");
    ...
}
```

- Реализовать функцию `SetupDataTriggers`, в которой создать для каждого типа экземпляр виджета с параметрами, сконфигурировать для него апдейтеры и добавить их на StackedWidget:

```cpp
void VsoSettingsView::SetupDataTriggers(Configuration::Data::VsoSettingsData &settings)
{
    for(auto& systemTypeAndParamsPair : settings.adjustments)
    {
	    // Создание экземпляра виджета с параметрами
        auto paramWidget = new VsoSystemParamsWidget(this);
        // Создание для виджета UiUpdaters и добавление их через метод базового класса
        AddUptaters(paramWidget->ConfigureUiUpdaters(systemTypeAndParamsPair.second));
        // Добавление параметров на StackedWidget
        AddToStackedWidget(paramWidget);
    }
}
```

![[ConfigurationSystem Diagramm]]