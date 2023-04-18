# bash_script with condittions
```
#!/bin/bash
Green='\033[0;92m'
Red='\033[0;91m'
Yellow='\033[0;33m'
NC='\033[0m' # No Color
current_time=$(date "+%Y.%m.%d-%H.%M.%S")
sum=0
for a in apache2 vsftpd
        do
        sum=`expr $sum + 1`
        which $a &> /dev/null
        if [ $? != 0 ] ; then
                echo -e "$sum:-${Red} $a packages is not available"     
                sleep 2
                echo -e "   ${Yellow} packages is going to install $NC"
                echo -e "    Please wait, it will take some time ............................."
                sudo apt install $a -y &>> /tmp/$a.installation.$current_time.log
                if [ $? == 0 ]
                then
                        echo -e "${Green}    Package $a is successfully installed $NC "
                else
                        echo -e "$Red Package $a installation failed. Please check logs in file: "/tmp/$a.installation.$current_time.log" for more details. $NC"

                fi
        else

                echo -e "$sum:-${Green} $a package is available no need to install $NC"
        fi
        echo ""
        sleep 2

done
```
