docker version
docker run -it ubuntu bash
docker pull hello-world
docker run hello-world

docker images
docker ps -a
docker inspect <container_id>

docker start -a <container_id> # -a = attach console / eklemezsen detached olarak çalışır arkada
docker logs <container_id> # detached console kayıtları

docker stop <container_id> #container durdurur

docker rm <container_id> # container ı siler
docker rm -f <container_id> # container çalışsa bile siler/force


docker run -p 8080:80 nginx # nginx latest ı indir ve çalıştır, 8080 potundan gelen istekleri de nginx 80 portuna yönlendir
docker exec -it <container_id> /bin/bash # -i interaktif -t terminal çalıştır
docker run -d -p 8080:80 nginx # deseydik detached modda açılırdı

docker kill <container_id> # container acil çıkış

<table>
  <thead>
    <tr>
      <th>Komut</th>
      <th>Açıklaması</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="highlighter-rouge">docker images</code></td>
      <td>Lokal registery’de mevcut bulunan Image’ları listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker ps</code></td>
      <td>Halihazırda çalışmakta olan Container’ları listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker ps -a</code></td>
      <td>Docker Daemon üzerindeki bütün Container’ları listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker ps -aq</code></td>
      <td>Docker Daemon üzerindeki bütün Container’ların ID’lerini listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker pull &lt;repository_name&gt;/&lt;image_name&gt;:&lt;image_tag&gt;</code></td>
      <td>Belirtilen Image’ı lokal registry’ye indirir. Örnek: <code class="highlighter-rouge">docker pull gsengun/jmeter3.0:1.7</code></td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker top &lt;container_id&gt;</code></td>
      <td>İlgili Container’da <code class="highlighter-rouge">top</code> komutunu çalıştırarak çıktısını gösterir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker run -it &lt;image_id|image_name&gt; CMD</code></td>
      <td>Verilen Image’dan terminal’i attach ederek bir Container oluşturur</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker pause &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı duraklatır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker unpause &lt;container_id&gt;</code></td>
      <td>İlgili Container <code class="highlighter-rouge">pause</code> ile duraklatılmış ise çalışmasına devam ettirilir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker stop &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı durdurur</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker start &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı durdurulmuşsa tekrar başlatır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rm &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı kaldırır fakat ilişkili Volume’lara dokunmaz</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rm -v &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı ilişkili Volume’lar ile birlikte kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rm -f &lt;container_id&gt;</code></td>
      <td>İlgili Container’ı zorlayarak kaldırır. Çalışan bir Container ancak <code class="highlighter-rouge">-f</code> ile kaldırılabilir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rmi &lt;image_id|image_name&gt;</code></td>
      <td>İlgili Image’ı siler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rmi -f &lt;image_id|image_name&gt;</code></td>
      <td>İlgili Image’ı zorlayarak kaldırır, başka isimlerle Tag’lenmiş Image’lar <code class="highlighter-rouge">-f</code> ile kaldırılabilir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker info</code></td>
      <td>Docker Daemon’la ilgili özet bilgiler verir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker inspect &lt;container_id&gt;</code></td>
      <td>İlgili Container’la ilgili detaylı bilgiler verir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker inspect &lt;image_id|image_name&gt;</code></td>
      <td>İlgili Image’la ilgili detaylı bilgiler verir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rm $(docker ps -aq)</code></td>
      <td>Bütün Container’ları kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker stop $(docker ps -aq)</code></td>
      <td>Çalışan bütün Container’ları kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rmi $(docker images -aq)</code></td>
      <td>Bütün Image’ları kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker images -q -f dangling=true</code></td>
      <td>Dangling (taglenmemiş ve bir Container ile ilişkilendirilmemiş) Image’ları listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker rmi $(docker images -q -f dangling=true)</code></td>
      <td>Dangling Image’ları kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker volume ls -f dangling=true</code></td>
      <td>Dangling Volume’ları listeler</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker volume rm $(docker volume ls -f dangling=true -q)</code></td>
      <td>Danling Volume’ları kaldırır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker logs &lt;container_id&gt;</code></td>
      <td>İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker logs -f &lt;container_id&gt;</code></td>
      <td>İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir ve <code class="highlighter-rouge">-f</code> follow parametresi ile o andan sonra oluşan logları da göstermeye devam eder</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker exec &lt;container_id&gt; &lt;command&gt;</code></td>
      <td>Çalışan bir Container içinde bir komut koşturmak için kullanılır</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker exec -it &lt;container_id&gt; /bin/bash</code></td>
      <td>Çalışan bir Container içinde terminal açmak için kullanılır. İlgili Image’da /bin/bash bulunduğu varsayımı ile</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">docker attach &lt;container_id&gt;</code></td>
      <td>Önceden detached modda <code class="highlighter-rouge">-d</code> başlatılan bir Container’a attach olmak için kullanılır</td>
    </tr>
  </tbody>
</table>


docker images # image listeler
docker tag a748835505b2 gsengun/myubuntu:0.1 # docker tag <image_id> <namespace>/<repo>:<tag> #kendi image ın için
docker rmi <image_id> # image silmek

###!!!###
Dockerfile metin bazlı fakat YAML, JSON, XML tarzı herhangi bir serializasyon formatı içermeyen satır bazlı olarak Instruction’ları
(komut) ayıran bir dosyadır. Genel olarak Instruction’ların formatı aşağıdaki gibidir. # ile başlayan bütün satırlar yorum olarak değerlendirilmektedir.
###!!!###



RUN # Build işlemi sırasında koşturulması gereken komutları belirtmek için kullanılır. apt-get xyz gibi

CMD #
  ~exec form:
              CMD [ "executable_file", "param1", "param2" ]
  ~ENTRYPOINT:
                ENTRYPOINT [ "ping" ]
                CMD [ "8.8.8.8" ]
  ~shell form:
              CMD command param1 param2

ENTRYPOINT #
  ~exec form:
              ENTRYPOINT ["executable", "param1", "param2"]
              ya da
              ENTRYPOINT [ "/bin/ping" ]
              docker run volkansahin/myubuntu:0.2 8.8.8.8
  ~shell form:
              ENTRYPOINT command param1 param2

EXPOSE#
    Default olarak Networking modülü Container’ların birbirlerinin UDP/TCP port’larına bağlanmalarına izin vermez.
    EXPOSE komutu ile ilgili portu (default TCP) belirtirler
     ya da Docker CLI’da --expose <port_number> ile başlatılmaları gereklidir.

     Docker’ın koşturulduğu host üzerinden Container’ların port’larına ulaşmak için Docker CLI’da Container başlatılırken
      -p <port_number> parametresinin verilmesi gereklidir.


ADD#
    Image’e Host dosya sisteminden veya internetten yeni bir dosya/klasör eklemek için
    Host klasörde bulunan ve Image’a kopyalanmak istenmeyen dosyalar .dockerignore dosyasının
     içinde belirtilebilir. Bu dosya tıplı .gitignore‘a benzemektedir.
    ADD ["<src>",... "<dest>"]
    ADD [ "https://curl.haxx.se/download/curl-7.50.1.tar.gz", "/tmp/curl.tar.gz" ]

COPY#
    ADD gibi ama netten dosya indiremez

WORKDIR#
     kendisinden sonra gelen RUN, CMD, ENTRYPOINT, COPY and ADD Instruction’larını etkiler
     WORKDIR /app/src
     ADD [ "./BuildDir/", "binaries/"]

HEALTHCHECK#
      servis çalışır durumda mı?
      HEALTHCHECK --interval=10s --timeout=60s --retries=1 CMD curl -f http://localhost:9876/ || exit 1
