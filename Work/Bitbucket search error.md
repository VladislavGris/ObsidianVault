## Related notes
- [[Microservices]]
- [[Microservices port clean]]

Bitbucket trying to use removed elasticsearch.
Content of `shared/bitbucket.properties`:
```
jdbc.driver=org.postgresql.Driver  
jdbc.url=jdbc:postgresql://primary:5432/bitbucket  
jdbc.user=limiteduser  
jdbc.password=NBRNgzznATn4f4wnskKFx8x  
server.port=7990  
server.secure=true  
server.proxy-port=443  
server.proxy-name=repo.okbtsp.com  
plugin.search.config.baseurl=http://elasticsearch:9200/  
plugin.search.config.username=bitbucket  
plugin.search.config.password=bitbucket
```
