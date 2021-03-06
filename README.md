# Deploy-MERN
# Connecting to the VPS
  VPS ကို connect လုပ်ဖိုဆိုရင် Sercer Ip ကို အသုံးပြုနိုင်ပါတယ်။ Root Password ကို create လုပ်ပြီး server ထဲကို Ip နဲ့  create လုပ်ခဲ့တဲ့ Password ကိုသုံးပြီး ဝင်နိုင်ပါတယ်။ ဒါပေမဲ့ ပိုပြီး secure ဖြစ်တဲ့ နည်းကတော့ SSH key ကို အသုံးပြုပြီး connect လုပ်တာပဲ ဖြစ်ပါတယ်။
# Creating SSH Key
## For MAC OS / Linux / Windows 10 (with openssh)
   1. Terminal App ကိုဖွင့်ပါ။
   2. `ssh-keygen -t rsa`
   3. key ကို default folder ဖြစ်တဲ့ /home/{your user name path}/.ssh/id_rsa မှာ  store လုပ်ဖို့ `ENTER` ကိုနှပ်ပါ။
   4. passphrase (တစ်နည်းအားဖြင့် ဒီ SSH key ရဲ့ password လို့ အလွယ်မှတ်နိုင်) ကို type လုပ်ပါ။ **< NOTE. ရိုက်လိုက်တဲ့ စာလုံးတွေ terminal တွင်မပေါ်ပါ။ >**
   5. passpharse ကို confirm လုပ်ပါ။ အောင်တွင်ပြထားသည့် စာလုံးတွေနှင့် ဆင်တူတဲ့ output ရပါလိမ့်မည် ->

     Your public key has been saved in /home/{your user name path}/.ssh/id_rsa .pub.
      The key fingerprint is:
      ae:89:72:0b:85:da:5a:f4:7c:1f:c2:43:fd:c6:44:30 name@example
      The key's randomart image is:
      +--[ RSA 2048]----+
      |                 |
      |         .       |
      |        E .      |
      |   .   . o       |
      |  o . . S .      |
      | + + o . +       |
      |. + o = o +      |
      | o...o * o       |
      |.  oo.o .        |
      +-----------------+ 
    6.`pbcopy < ~/.ssh/id_rsa.pub` ကိုသုံးပြီး SSH Key ကို copy လုပ်ပါ။

## For Windows

  1. PuTTY and PuTTYgen ကို download လုပ်ပါ။
  2. PyTTYgen ကို ဖွင့်ပြီး Generate ကိုနှိပ်ပါ။
  3. key ကို copy လုပ်ပါ။ 
  4. passphrase ကို သတ်မှတ်ပါ။ confirm လုပ်ပါ။
  5. private key နဲ့ public key ကို Save လုပ်ပါ။

## Connection

   SSH key ကို copy လုပ်ပြီး ကိုယ် ဝယ်ထားတဲ့ hosting service privider (eg. digitalocean, hostinger) ရဲ့ dashboard က SSH key နေရာမှာ ထည့်ပါ။ save လုပ်ပါ။ 

### For MAC OS / Linux

    ```
    sudo ssh -i ~{SSH-key-path}  {username}@{vps-IP}
    ```
    
### For Windows

   1. PuTTY app ကိုဖွင့်ပါ။
   2. IP address ကိုဖြည့်ပါ။
   3. Connection -> SSH -> Auth ကိုသွားပါ။
   4. Browse ကိုနှိပ်ပြီး private key save ထားတဲ့ file လမ်းကြောင်းကို ရွေးပေးပါ။

# First Configuration
## Deleting apache server

   တစ်ချို့  hosting တွေမှာ apache server တစ်ခါတည်း  install ထားပီးသား ပါတတ်ပါတယ်။ apache serverကို သုံးမယ်ဆိုရင် ဒီ အဆင့်ကို လုပ်စရာမလိုပါ။ 
   ဒီမှာတော့ Nginx ကိုသုံးမှာ ဖြစ်တဲ့ အတွက် apache server ကို delete လုပ်မှာပါ။

   ```
   systemctl stop apache2
   ```
   
   ```
   systemctl disable apache2
   ```
   
   ```
   apt remove apache2
   ```
   
   သက်ဆိုင်ရာ dependencies တွေကို delete လုပ်ဖို့အတွက်
   
   ```
   apt autoremove
   ```
   
## Cleaning and updating server

   ```
   apt clean all && sudo apt update && sudo apt dist-upgrade
   ```
   
   ```
   rm -rf /var/www/html
   ```
   
## Installing Nginx

   ```
   apt install nginx
   ```

## Installing and configure Firewall

   ```
   apt install ufw
   ```
   
   ```
   ufw enable
   ```
   
   ```
   ufw allow "Nginx Full"
   ```
   terminal က SSH client ဝင်လို့မရ ပါက port 22 ကို allow လုပ်ပေးဖို့ လိုပါတယ်။

## First Page
### Delete the default server configuration
   
   /etc/nginx/sites-available/default ကို edit လုပ်ပြီး သုံလို့ ရပေမဲ့ project တစ်ခု မက သုံး တဲ့ အခါ အဆင်ပြေ အောင် default file ကို ဖျက်ပြီး အသစ် လုပ်ပါမယ်။
   
   ```
   rm /etc/nginx/sites-available/default
   ```
   
   ```
   rm /etc/nginx/sites-enabled/default
   ```
   
### First configuration
 
   ```
    nano /etc/nginx/sites-available/ecommerce
   ```
   
    ```
    server {
      listen 80;

      location / {
           root /var/www/netflix;
           index  index.html index.htm;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
           try_files $uri $uri/ /index.html;
      }
    }
  
   
   sites-available ထဲမှာ ရေးသမျှ sites-enabled ထဲမှာလဲ တစ်ခါတည်း ပြင်သွား ဖို့ အတွက်
   
    ```
    ln -s /etc/nginx/sites-available/ecommerce /etc/nginx/sites-enabled/ecommerce
    ```
    
### Write your fist message

    ```
    nano /var/www/ecommerce/index.html
    ```

### Start Nginx and IP address ကို browser မှာ ရိုက်ပြီး ကြည့်ပါ။

    ```
    systemctl start nginx
    ```
# Uploading Apps Using Git

repository မှာ project forder တွေကို တင်ပြီးပီလို့ ယူဆပါမယ်။

 > *note
 > - local မှာ port ခွဲ သုံးမှာ ဖြစ်တွက် အတွက် NodeJs project ရဲ့ index.js or server.js မှာ `app.use(cors());` ကိုသုံးရပါမယ်
 > - React router တွေ အတွက် react project တွေရဲ့ `package.json` file မှာ `"homepage": ".",` ထည့်ပေးရပါမယ်။ *
   

  ```
  apt install git
  ```
  
  ```
  mkdir ecommerce
  ```
  
  ```
  cd ecommerce
  ```
  
  ```
  git clone <your repository>
  ```

## Nginx Configuration for Nodejs Api apps

   ```
   nano /etc/nginx/sites-available/netflix
   ```
   
   ```
   location /api {
        proxy_pass http://{IP- Address}:{App port};
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
  }
  ```

  browser မှာ ip-address/api ကို ခေါ်ကြည့်ရင် `502` error ကို တွေရမှာပါ။ configuration လုပ်တာ အောင်မြင် ပါတယ်။ App ကို run ဖို့ install အနည်းငယ်လုပ်ဖို့ လိုပါသေးတယ်။
  
  ```
  apt install nodejs
  ```
  
  ```
  apt install npm
  ```
  
  ```
  cd {app folder}
  ```
  
  ```
  npm install
  ```
  
  ```
  nano .env
  ```
  .env ထဲက code တွေကူး ထည့်ပြီး save ပါ။
  
  > *App ကို မ run ခင် mongodb atlas သုံးထားရင် IP list မှာ VPS IP Address ကို ထည့်ပေးဖို့လိုပါတယ်။*
  
  ```
  node index.js
  ```

### SSH session || terminal ကို ပိတ်လိုက်ရင် app က အလုပ် လုပ်တော့မှာ မဟုတ်ပါဘူး။ ဒါကို ပြင်ဖို့ Pm2 ဆိုတဲ့ package ကို install လုပ်ရပါမယ်

  ```
  npm i -g pm2
  ```
  
  pm1 instance အသစ် create ရပါမယ်။
  
  ```
  pm2 start --name api index.js 
  ```
  
  ```
  pm2 startup ubuntu 
  ```
  
  # React App Deployment
  
  React app folder ထဲ သို့ သွားပါ
  
  ```
  cd {your folder name}
  ```
  .env file ရှိရင် `nano .env` နဲ့ create လုပ်ပြီး copy လုပ်ပါ။
  
  ```
  npm install
  ```

 Create Build file

  ```
  npm run build
  ```
build file ကို main web file ထဲကို move မယ်။

 ```
 rm -rf /var/www/netflix/*
 ```
 
 ```
 mkdir /var/www/ecommerce/ecommerce_front_end
 ```
 ```
 cp -r build/* /var/www/ecommerce/ecommerce_front_end
 ```
 
 Change server configuration
 
 ```
 nano /etc/nginx/sites-available/ecommerce
 ```
 
 ```
  location / {
        root /var/www/ecommerce/ecommerce-front-end/;
        index  index.html index.htm;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        try_files $uri $uri/ /index.html;
  }
  ```
