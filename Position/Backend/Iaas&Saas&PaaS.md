
## Infrastructure as a Service(IaaS)
AWS는  infrastructure as a Service(IaaS)라고 부르는데, 사용자가 OS, 배포되는 응용SW뿐 만 아니라 방화벽, 포트, 스케일링 등 디테일하게 설정이 가능하고, 배포에 필요한 과정들도 직접 해야됨. git도 설치가 안되어있으니 그런것도 리눅스환경에서 설치해야하고, node 등 사용한 프레임워크와 관련된 디펜던시들을 하나하나 설정해줘야함. 물론 개발파일을 업로드하고 구동하는것도 수동!


## Platform as a Service(Paas)
Heroku, FIrebase같은걸 Platform as a sservice (PaaS)라고 하는데, AWS에서 복잡한 설정 및 설치,배포/구동 과정을 해당 서비스 차원에서 auto-detect해서 작업해줌! 그래서 파일만 업로드하고 어떤 프레임워크 썻는지만 설정하면 바로 구동가능!

가격은 당연히 PaaS가 더 높은편이나 구동까지 걸리는 시간이 절약됨. 반면 IaaS는 설정이 힘들지만 디테일하게 설정할 수 있어서 가격대비 성능이 뛰어나고 유지보수에 용이함.

Heroku같은 플랫폼이 AWS를 기반으로 돌아감!

## Software as a Service (Saas)

인터넷을 통해 어플리케이션을 제공하는 형식.

ie. Salesforce, Google Workspace apps(SpreadSheet etc), Microsoft 365