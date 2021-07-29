# Deploy-MERN
# Connecting to the VPS
  VPS ကို connect လုပ်ဖိုဆိုရင် Sercer Ip ကို အသုံးပြုနိုင်ပါတယ်။ Root Password ကို create လုပ်ပြီး server ထဲကို Ip နဲ့  create လုပ်ခဲ့တဲ့ Password ကိုသုံးပြီး ဝင်နိုင်ပါတယ်။ ဒါပေမဲ့ ပိုပြီး secure ဖြစ်တဲ့ နည်းကတော့ SSH key ကို အသုံးပြုပြီး connect လုပ်တာပဲ ဖြစ်ပါတယ်။
# Creating SSH Key
## For MAC OS / Linux / Windows 10 (with openssh)
   1. Terminal App ကိုဖွင့်ပါ။
   2. `ssh-keygen -t rsa`
   3. key ကို default folder ဖြစ်တဲ့ /home/{your user name path}/.ssh/id_rsa မှာ  store လုပ်ဖို့ `ENTER` ကိုနှပ်ပါ။
   4. passphrase (တစ်နည်းအားဖြင့် ဒီ SSH key ရဲ့ password လို့ အလွယ်မှတ်နိုင်) ကို type လုပ်ပါ။ **NOTE.ရိုက်လိုက်တဲ့ စာလုံးတွေ terminal တွင်မပေါ်ပါ**
