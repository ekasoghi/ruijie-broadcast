Ruijie Cloud Broadcast Server Installation Guide on VPS and Local
STEP 1 - Ubuntu VPS Preparation:
--------------------------------
1. Login to your VPS
2. Run:
sudo apt update && sudo apt install nginx git python3-pip -y
3. Upload and extract the ruijie_broadcast.zip file:
unzip ruijie_broadcast.zip
cd ruijie_broadcast
4. Install Python dependencies:
pip3 install flask requests gunicorn
5. Run the application:
gunicorn --bind 0.0.0.0:8080 app:app
6. Setup Nginx (optional if using a domain):
sudo nano /etc/nginx/sites-available/ruijie
(Fill in the configuration according to the previous instructions)
STEP 2 - Configure the config.py File:
----------------------------------------
- Fill in your Ruijie and Wablas API Key:
RUIJIE_API_KEY = 'isi_api_key'
WABLAS_TOKEN = 'isi_token_wablas'
STEP 3 - Automatic Cron Broadcast (Optional):
-----------------------------------------------
crontab -e
Add:
*/10 * * * * curl http://localhost:8080/
STEP 4 - Setup Captive Portal Redirect in Ruijie Cloud:
----------------------------------------------------------
- Redirect the captive portal to:
https://wifi.yourbusiness.com/landing?mac={client_mac}&ip={client_ip}
STEP 5 - Local Mode (Optional if the gateway supports local redirect):
------------------------------------------------------------------
- Create a local server with Nginx
- Redirect users to:
https://wifi.yourbusiness.com/landing
DONE! Ruijie WiFi broadcast system is active.
Contact the developer if you want full integration to ERP, dynamic landing pages, or advanced user tracking.
