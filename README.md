# Docker

#### Install Docker in Centos
	[user@machine docker]$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
  [user@machine docker]$ sudo yum install docker-ce
  [user@machine docker]$ sudo chown <user>:<user> -R docker
  [user@machine docker]$ sudo usermod -a -G docker <user>
	[user@machine docker]$ sudo systemctl status docker
  [user@machine docker]$ sudo systemctl start docker


#### Run Docker
	[user@machine docker]$ docker pull alpine
	docker images
	REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	alpine              latest              caf27325b298        11 days ago         5.53MB
	hello-world         latest              fce289e99eb9        5 weeks ago         1.84kB

	[user@machine docker]$ docker run hello-world
    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
     3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
     $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
     https://hub.docker.com/

    For more examples and ideas, visit:
     https://docs.docker.com/get-started/

	[user@machine docker]$ docker ps -a
	CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
	7d1f1fc9edc1        hello-world         "/hello"            2 seconds ago       Exited (0) 1 second ago                       vigilant_boyd


#### Update Docker config
    [user@machine docker]$ sudo vi /usr/lib/systemd/system/docker.service
    [user@machine docker]$ sudo systemctl daemon-reload
    [user@machine docker]$ sudo systemctl restart docker
    [user@machine docker]$ docker info
  
  
#### Add 192.168.X.Y as proxy
	[user@machine docker]$ sudo vi /etc/systemd/system/docker.service.d/http-proxy.conf
	[user@machine docker]$ cat /etc/systemd/system/docker.service.d/http-proxy.conf
    [Service]
    Environment=http_proxy=http://192.168.X.Y:3128/
    Environment=https_proxy=http://192.168.X.Y:3128/
    Environment=no_proxy=localhost,127.0.0.1


#### Add 192.168.232.147 Proxy CA Certificate
	[user@machine docker]$ sudo cp proxy.cer /etc/pki/ca-trust/source/anchors/
	[user@machine docker]$ update-ca-trust    
    [user@machine docker]$ cat proxy.cer
    -----BEGIN CERTIFICATE-----
    MIID+DCCAuCgAwIBAgIEKxWMgDANBgkqhkiG9w0BAQsFADBdMQswCQYDVQQGEwIg
    IDEfMB0GA1UEChMWQmx1ZSBDb2F0IFNHLVZBIFNlcmllczETMBEGA1UECxMKMTAw
    MzU5ODk1MzEYMBYGA1UEAxMPMTkyLjE2OC4yMzIuMTQ3MB4XDTE4MTEyNzAyNDgz
    MloXDTIwMTEyNjAyNDgzMlowXTELMAkGA1UEBhMCICAxHzAdBgNVBAoTFkJsdWUg
    Q29hdCBTRy1WQSBTZXJpZXMxEzARBgNVBAsTCjEwMDM1OTg5NTMxGDAWBgNVBAMT
    DzE5Mi4xNjguMjMyLjE0NzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
    AKJuNh0WFW2j0wbWd2qvwQ47eLYigwDefwQKffhmBRqG5rEJ1knhgUcR66uzHw04
    GkC/deRvDHVqWm1MhQbbLVSQW0NHuUEGsue5UL+FFZ5W/DlSrWYTdrO9waZNC57X
    X8i3Whpkma2zWEEQEbGFMjpwS8La8lIJko6cNEfwr+mWH9WiIYGgFnRHH3x+opcO
    DVzg119OSecNvPftxtYG5eHXGPxm2RRvDxwbIAeWfNnQwCbB2pzeKDN2gaeQHVVm
    +zNwdyySIqWJd2F190ecaw4n9IvxMofsas1XpYJHTLjUauXBXIDkhDdsIMVW3P4I
    xusuPFacTB4RB4xvPNWqn4ECAwEAAaOBvzCBvDAdBgNVHQ4EFgQUwuunGvn1VsVG
    WbFXNOCd2XXVh7IwgYkGA1UdIwSBgTB/gBTC66ca+fVWxUZZsVc04J3ZddWHsqFh
    pF8wXTELMAkGA1UEBhMCICAxHzAdBgNVBAoTFkJsdWUgQ29hdCBTRy1WQSBTZXJp
    ZXMxEzARBgNVBAsTCjEwMDM1OTg5NTMxGDAWBgNVBAMTDzE5Mi4xNjguMjMyLjE0
    N4IEKxWMgDAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3DQEBCwUAA4IBAQAFUEFv
    /AWre7+/wq5Ig3fl1G5WQtWE8s/FMwRJ8gMTUhXkp462ZYPIMs/UkCks3DQ+7SWJ
    G+Ar76wImOn8rihbOKlJ4YAZfwMuDfxGxywZxJpc76wtY7QuS+lJUXnRkiqyGcQj
    VUWC9cTfiwVaZmLQ8JWTYFd+2LdAeIqHejwmESybqyLN43T8sMx7OiPiIQc8Lg2I
    ZHJFirrNIBoLRvBfHR8f6ZqWGygVlBztXw2t7OC7Wps/b3HsI10IB2jAnUjb3yf1
    fdM2Ug8WuG5IUlLk09U7b7eG5LzFrxuwRL41491bs8Lu3zPGrg8MVtBSGAUIRcsk
    6AbR7V2u+PDCnNFW
    -----END CERTIFICATE-----


#### Run GUI Application in Docker Container
    [user@machine gui-app]$ cat Dockerfile
    FROM centos
    ENV http_proxy http://192.168.195.153:3128
    ENV https_proxy http://192.168.195.153:3128
    RUN yum install -y xeyes
    CMD ["/usr/bin/xeyes"]
    
    [user@machine gui-app]$ docker build -t gui-app .
    [user@machine gui-app]$ docker run --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" gui-app


#### Run C++ with Boost
    [user@machine docker]docker build --file Dockerfile_c-plus-plus-with-boost --tag c-plus-plus-with-boost .
    [user@machine docker]docker build --file Dockerfile_boost-test --tag boost-test .
    [user@machine docker]docker run --rm -it boost-test:latest /bin/bash
    root@6616ea04a9c3:/home# BoostTest -v 1234


    **** Start ****


    Command line value: 1234

    Parallelization with OpenMP test...

    Loop 1 through 10 in parallel and print to STDOUT (not necessarily in order)...

    7
    8
    9
    10
    1
    2
    3
    4
    5
    6


    **** Done ****

    root@6616ea04a9c3:/home#


#### Jupyter in Docker
	# create a directory
	mkdir work
	# give the default jovyan (uid=1000) user ownership
	sudo chown 1000 work
	# start the container with the host work folder mounted
	docker run -it --rm -p 18888:8888 -v `pwd`/work:/home/jovyan/work jupyter/datascience-notebook
