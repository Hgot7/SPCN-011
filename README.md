# SPCN-011
ขั้นตอนการใช้งานของสร้าง vm and ct on Proxmox cluster

1) Create master vm [ ubuntu-22.04 ]
   - สร้าง master vm มา 1 ตัว แล้วทำการ set ค่าพื้นฐานต่างๆ
   - เช็คเวลาด้วย dateและset update time ด้วยคำสั่ง sudo timedatectl set-timezone Asia/Bangkok
   - ทำการเปิดใช้งาน ip qemu ด้วยคำสั่ง
       - sudo -i
       - apt update
       - apt install qemu-guest-agent
       - systemctl enable qemu-guest-agent
       - และทำการตั้งค่าที่ option ให้เปิดใช้งานตัว Qemu guest agent เป็น Enable 
       ![master](https://user-images.githubusercontent.com/117428887/207249679-cc1c035d-567c-47c2-bb70-4af156fbd084.png)
       - reboot เพื่อรีระบบ
   1.1) clone from template 2 vm
   - Click ที่ vm(master) > Convert to template
   -  หลังจาก vm(master) กลายเป็นtemplate ให้ Click vm แล้วเลือก Clone เป็นตัวvmใหม่2ตัว
   
      ![click_clone](https://user-images.githubusercontent.com/117428887/207249801-0fdeac3a-f89a-4d63-beb7-018d4e3c5cf7.png)   
   - ทำการsetระบบโดย
        - date เพื่อเช็ค timezone
          ![date](https://user-images.githubusercontent.com/117428887/207250064-7dbee734-ba17-4e07-8c8e-bfc448aed275.png) 
        - ทำการเปลี่ยนipของระบบเพื่อไม่ให้ipซ้ำกันโดย
            - sudo -i
            - rm /var/lib/dbus/machine-id
            - nano /etc/machine-id เพื่อลบ id เก่าออก
            - ln -s /etc/machine-id /var/lib/dbus/machine-id เพื่อ link เชื่อมต่อกับ machine-id
            - reboot เพื่อรี ip ใหม่
            - หลังเปลี่ยน ip clone1
              ![clone1](https://user-images.githubusercontent.com/117428887/207249927-11b31df4-b640-437e-925d-366fdff1e0a8.png)
            - หลังเปลี่ยน ip clone2
              ![clone2](https://user-images.githubusercontent.com/117428887/207250128-efab9275-9ffb-4829-81d6-709189a7d3db.png)
 
2) create vm from other os
   - Create VM จากนั้นทำการตั้งค่าที่กำหนดโดยระบบปฏิบัติการที่เลือกใช้คือ Kali
      - Summary ของ Linux Mint
        ![image](https://user-images.githubusercontent.com/117428887/207254087-5c33fc7e-9147-4fe2-ba37-0b3760e770ab.png)
      - หน้า console screen
        ![image](https://user-images.githubusercontent.com/117428887/207250406-0046c82f-bab3-4619-b8b3-40d1d6c397ec.png)  

3) create container template 
   - Click create container template เพื่อสร้าง CT
      - Summary 
        ![image](https://user-images.githubusercontent.com/117428887/207257544-a0089b6a-1db7-40a6-b2f2-47f3c7c7357e.png)
      - console screen 
        ![image](https://user-images.githubusercontent.com/117428887/207257761-fc2e8d1c-a456-4780-8b78-65498a3769db.png)
