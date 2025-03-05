В руководстве к [диагностической программе БИНС](https://wiki.okbtsp.com/spaces/BM9A33MB/pages/143327394/%D0%91%D0%B8%D0%BD%D1%817?preview=/143327394/143327395/%D0%9F%D0%B0%D1%81%D0%BB%D1%8F%D0%B4%D0%BE%D1%9E%D0%BD%D0%B0%D1%81%D1%86%D1%8C%20%D0%B4%D0%B7%D0%B5%D1%8F%D0%BD%D0%BD%D1%8F%D1%9E%20%D0%BF%D1%80%D1%8B%20%D0%BF%D1%80%D0%B0%D1%86%D1%8B%20%D0%B7%20%D0%91%D0%86%D0%9D%D0%A1-7.docx) есть пример GUI:
![[Pasted image 20250305120518.png]]
В статус баре есть три именованные строки:
- БИНС и СНС - статусные данные БИНС и СНС. В CanGlobal содержатся в единой структуре [Pgn46B_SinsState](https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/CanGlobal/CanGlobal_Sins.h#325).
- ДПЦ
Отдельно раположена неименованная строка с флагами, которые соответствуют значениям структуры [Pgn469_SinsFlags](https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/CanGlobal/CanGlobal_Sins.h#280).