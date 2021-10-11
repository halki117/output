- ec2（パブリックサブネット側）にsshアクセス

- var/wwwデレクトリー作成
  ```
  [ec2-user@ip-10-0-0-240 ~] mkdir /var/www
  ```
  
- var/wwwディレクトリに移動し,githubからプロジェクトをコピー
  ```
  [ec2-user@ip-10-0-0-240 ~] $ cd /var/www
  [ec2-user@ip-10-0-0-240 www] $ git clone プロジェクトurl
  ```
  
- PHPのイメージを作成し、コンテナを起動
  ```
  [ec2-user@ip-10-0-0-240 www] $ docker image build -t aws_task2_php ./docker/php
  [ec2-user@ip-10-0-0-240 www] $ docker run --name aws_task2_phpContainer -v /var/www/laravel_task4:/src -d aws_task2_php
  ```
  
- phpコンテナの中に入ってIPアドレスを調べる、
  ```
  [ec2-user@ip-10-0-0-240 www] $ docker exec -it aws_task2_phpContainer bash
  root@a9f0e8f2c37b:/src# hostname -i
  root@a9f0e8f2c37b:/src# exit
  ```

- nginxディレクトリのdefault.confの下記の部分を調べたIPアドレスに書き換える
  ```
  fastcgi_pass <調べたIPアドレス>:9000;
  ```

- nginxのイメージを作成し、コンテナを起動
  ```
  [ec2-user@ip-10-0-0-240 www]$ docker image build -t aws_task2_nginx ./docker/nginx
  [ec2-user@ip-10-0-0-240 www]$ docker run --name aws_task2_nginxContainer -v /var/www/laravel_task4:/src -p 80:80 -d aws_task2_nginx
  ```
  
- パブリックサブネット側のEC2を踏み台にプライベートサブネットのEC2へアクセス。
  コンテナは構築せずに直接mysqlをインストール
  参考記事: https://nogson2.hatenablog.com/entry/2020/04/26/215047
  
  
  
  
  
 <br>
 <br>
 <br>
 
- phpコンテナにアクセスしてstorageの権限を変更した<br>
 [ec2-user@ip-10-0-0-240 www]$ docker exec -it aws_task2_nginxContainer bash
 root@a9f0e8f2c37b:/src# chmod -R 777 storage
 
 ※アプリの固有キーを生成。これがないとエラーになる。<br>
 root@a9f0e8f2c37b:/src# php artisan key:generate
 Application key set successfully.


<br>
<br>
<br>
データベースにアクセスしてrootユーザーに対して外部からアクセスできる様に設定をした。
参考記事: https://teratail.com/questions/45324
grant all privileges on *.* to 'root'@'10.0.0.240' identified by 'root' with grant option;
