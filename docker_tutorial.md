|  |   |
|---|---|
| docker version  |   |
| docker run -it ubuntu bash  |   |
| docker pull hello-world  |   |
|docker images |Image’lari listeler |
|docker ps | çalismakta olan Container’lari listeler|
|docker ps -a| Docker Daemon üzerindeki bütün Container’lari listeler|
|docker ps -aq| bütün Container’larin ID’lerini listeler|
|docker inspect <container_id> | |
|docker start -a <container_id> |-a = attach console / eklemezsen detached olarak çalisir arkada |
|docker logs <container_id> | detached console kayitlari|
|docker stop <container_id> | container durdurur|
|docker rm <container_id> |container i siler |
| docker rm -f <container_id>| container çalissa bile siler/force|
| docker run -p 8080:80 nginx| nginx latest i indir ve çalistir, 8080 potundan gelen istekleri de nginx 80 portuna yönlendir |
|docker exec -it <container_id> /bin/bash |-i interaktif -t terminal çalistir |
| docker run -d -p 8080:80 nginx|deseydik detached modda açilirdi |
| docker kill <container_id>| container acil çikis|
|docker pull <repository_name>/<image_name>:<image_tag> | Belirtilen Image’i lokal registry’ye indirir. Örnek: docker pull gsengun/jmeter3.0:1.7|
|docker top <container_id> |Ilgili Container’da top komutunu çalistirarak çiktisini gösterir |
|docker run -it <image_id|image_name> CMD | Verilen Image’dan terminal’i attach ederek bir Container olusturur|
| docker pause <container_id>| Ilgili Container’i duraklatir|
| docker unpause <container_id>|Ilgili Container pause ile duraklatilmis ise çalismasina devam ettirilir|
|docker stop <container_id> |Ilgili Container’i durdurur |
| docker start <container_id>|Ilgili Container’i durdurulmussa tekrar baslatir |
|docker rm <container_id> | Ilgili Container’i kaldirir fakat iliskili Volume’lara dokunmaz|
|docker rm -v <container_id> |Ilgili Container’i iliskili Volume’lar ile birlikte kaldirir |
|docker rm -f <container_id> |Ilgili Container’i zorlayarak kaldirir. Çalisan bir Container ancak -f ile kaldirilabilir |
|docker rmi <image_id|image_name> |Ilgili Image’i siler |
|docker rmi -f <image_id|image_name> | Ilgili Image’i zorlayarak kaldirir, baska isimlerle Tag’lenmis Image’lar -f ile kaldirilabilir|
|docker info |Docker Daemon’la ilgili özet bilgiler verir |
|docker inspect <container_id> | Ilgili Container’la ilgili detayli bilgiler verir|
| docker inspect <image_id|image_name>|Ilgili Image’la ilgili detayli bilgiler verir |
| docker rm $(docker ps -aq)| Bütün Container’lari kaldirir|
|docker stop $(docker ps -aq) |Çalisan bütün Container’lari kaldirir |
|docker rmi $(docker images -aq) |Bütün Image’lari kaldirir |
|docker images -q -f dangling=true | Dangling (taglenmemis ve bir Container ile iliskilendirilmemis) Image’lari listeler|
| docker rmi $(docker images -q -f dangling=true)|Dangling Image’lari kaldirir |
| docker volume ls -f dangling=true| Dangling Volume’lari listeler|
|docker volume rm $(docker volume ls -f dangling=true -q)| Danling Volume’lari kaldirir|
|docker logs <container_id> |Ilgili Container’in terminalinde o ana kadar olusan çiktiyi gösterir |
|docker logs -f <container_id> |Ilgili Container’in terminalinde o ana kadar olusan çiktiyi gösterir ve -f follow parametresi ile o andan sonra olusan loglari da göstermeye devam eder |
| docker exec <container_id> <command>|Çalisan bir Container içinde bir komut kosturmak için kullanilir |
|docker exec -it <container_id> /bin/bash | Çalisan bir Container içinde terminal açmak için kullanilir. Ilgili Image’da /bin/bash bulundugu varsayimi ile|
|docker attach <container_id> | Önceden detached modda -d baslatilan bir Container’a attach olmak için kullanilir|
|docker rmi <image_id> |  image silmek|



###!!!###
Dockerfile metin bazli fakat YAML, JSON, XML tarzi herhangi bir serializasyon formati içermeyen satir bazli olarak Instruction’lari
(komut) ayiran bir dosyadir. Genel olarak Instruction’larin formati asagidaki gibidir. # ile baslayan bütün satirlar yorum olarak degerlendirilmektedir.
###!!!###



####RUN 
    Build islemi sirasinda kosturulmasi gereken komutlari belirtmek için kullanilir. apt-get xyz gibi

####CMD
    ~exec form:
              CMD [ "executable_file", "param1", "param2" ]
    ~ENTRYPOINT:
                ENTRYPOINT [ "ping" ]
                CMD [ "8.8.8.8" ]
    ~shell form:
              CMD command param1 param2

####ENTRYPOINT
    ~exec form:
              ENTRYPOINT ["executable", "param1", "param2"]
              ya da
              ENTRYPOINT [ "/bin/ping" ]
              docker run volkansahin/myubuntu:0.2 8.8.8.8
  ~shell form:
              ENTRYPOINT command param1 param2

####EXPOSE
    Default olarak Networking modülü Container’larin birbirlerinin UDP/TCP port’larina baglanmalarina izin vermez.
    EXPOSE komutu ile ilgili portu (default TCP) belirtirler
     ya da Docker CLI’da --expose <port_number> ile baslatilmalari gereklidir.

     Docker’in kosturuldugu host üzerinden Container’larin port’larina ulasmak için Docker CLI’da Container baslatilirken
      -p <port_number> parametresinin verilmesi gereklidir.


####ADD
    Image’e Host dosya sisteminden veya internetten yeni bir dosya/klasör eklemek için
    Host klasörde bulunan ve Image’a kopyalanmak istenmeyen dosyalar .dockerignore dosyasinin
     içinde belirtilebilir. Bu dosya tipli .gitignore‘a benzemektedir.
    ADD ["<src>",... "<dest>"]
    ADD [ "https://curl.haxx.se/download/curl-7.50.1.tar.gz", "/tmp/curl.tar.gz" ]

####COPY
    ADD gibi ama netten dosya indiremez

####WORKDIR
     kendisinden sonra gelen RUN, CMD, ENTRYPOINT, COPY and ADD Instruction’larini etkiler
     WORKDIR /app/src
     ADD [ "./BuildDir/", "binaries/"]

####HEALTHCHECK
      servis çalisir durumda mi?
      HEALTHCHECK --interval=10s --timeout=60s --retries=1 CMD curl -f http://localhost:9876/ || exit 1
