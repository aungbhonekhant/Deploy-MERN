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

     Your public key has been saved in /Users/lamadev/.ssh/id_rsa.pub.
      The key fingerprint is:
      ae:89:72:0b:85:da:5a:f4:7c:1f:c2:43:fd:c6:44:30 lamadev@mac.local
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

##For Windows
1. PuTTY and PuTTYgen ကို download လုပ်ပါ။
2. PyTTYgen ကို ဖွင့်ပြီး Generate ကိုနှိပ်ပါ။
