### Задание 1
![image](https://github.com/user-attachments/assets/db79ba58-7e11-4b5c-a4f8-88a272cedb6b)
![image](https://github.com/user-attachments/assets/d427fff1-e99e-4cb5-a60d-5b5e5d16ffbc)
![image](https://github.com/user-attachments/assets/3570ef49-b55b-43b5-9e8d-c574b900a6db)
Обрываем другой 
![image](https://github.com/user-attachments/assets/12ae224c-b843-48e5-b38f-52d19bd88c87)
[hsrp_advanced.zip](https://github.com/user-attachments/files/20035742/hsrp_advanced.zip)



### Задание 2

![Ubuntu 1-2025-05-13-14-27-27](https://github.com/user-attachments/assets/3c374420-6b52-4a7d-86c3-65aede8c25ad)
![ Ubuntu 2-2025-05-13-14-26-23](https://github.com/user-attachments/assets/01cefe77-08a4-46c8-807e-79edab2c2d06)
![ Ubuntu 2-2025-05-13-14-28-28](https://github.com/user-attachments/assets/402e6938-283f-4e41-b375-cbd1e42d971c)
/etc/keepalived/keepalived.conf:
global_defs {
    script_user root
    enable_script_security
}

vrrp_script check {
    script "/etc/keepalived/check.sh"
    interval 3
    fall 2
    rise 2
}

vrrp_instance VI_1 {
    state MAIN / BACKUP
    interface ens33
    virtual_router_id 15
    priority 255/200
    advert_int 1

    virtual_ipaddress {
        192.168.88.15/24
    }

    track_script {
        check
    }
}
check.sh:
#!/bin/bash

PORT=80
WEB_ROOT="/var/www/html"
INDEX_FILE="$WEB_ROOT/index.html"

if ! nc -z 127.0.0.1 $PORT; then
    exit 1
fi

if [ ! -f "$INDEX_FILE" ]; then
    exit 1
fi

exit 0
