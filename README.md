## Hadoop 설치하기 
 ```sh 
 
 
 [기존 java 삭제하기] # centos 경우에는 자바 설치가 되어 있지 않으므로 따로 실행할 필요 없음 
 
 
 yum -y remove "java-*" 
 
 
 ``` 
 
 
     1. jdk 다운로드 
 ``` 
 
 
 arch명령어를 통해 비트수 확인 후 설치 
 
 
 ``` 
 
 
 ```sh 
 
 
     cd ~/Downloads 
 
 
     (64비트인 경우) 
     wget —no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz 
 
 
     (32비트인 경우) 
     wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-i586.tar.gz" 
      
 
 
     cd ~/Downloads/ 
     tar –zxvf jdk-8u5-linux-x64.tar.gz 
     mkdir /usr/java 
     mv jdk1.8.0_05 /usr/java/jdk1.8 
 
 
     vi /etc/profile 
 
 
     밑에 export 3줄만 추가 
 
 
     export JAVA_HOME=/usr/java/jdk1.8 
     export PATH=$JAVA_HOME/bin:$PATH 
     export CLASSPATH=$CLASSPATH:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar 
 
 
     # 실행 
     source /etc/profile 
      
 ``` 
 
 
     2. 계정 추가하기 
      
 ```sh 
    
   - SSH 설치 및 공개 키 설정  
   - Hadoop클러스터에서 Master와 Slave들 간에 통신은 SSH를 이용함 
   - 모든 컴퓨터에는  SSH가 설치되어 있어야 함 
   - Master에서 암호없이 Slave에 접속하기 위해서 공개 키가 필요함 
    
     useradd hadoop 
     su - hadoop 
     ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa 
     cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys 
     chmod 0600 ~/.ssh/authorized_keys 
      
 ``` 
      
     3. 로컬호스트 들어갔다 나오기 
 ```sh 
 
 
     ssh localhost 
     exit 
      
 ``` 
 
 
 ```sh 
 
 <- 여기까지 hadoop 계정 [hadoop@localhost ~] 
 
 ```
 ```sh
 
 -> 지금부터 root 계정으로 
   > su 
   > password 
   =[root@localhost hadoop] 
    
 ``` 
 
 
     4. 하둡다운로드 
      
 ```sh 
 
 
     cd /home 
     mkdir hadoop 
     cd hadoop 
     wget http://apache.tt.co.kr/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz 
     tar -zxvf hadoop-2.7.1.tar.gz 
      
 ``` 
