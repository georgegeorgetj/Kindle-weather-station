# Kindle-weather-station

Permet d’afficher la météo depuis une station Netatmo sur un Kindle.

Le résultat d’un jour de pluie est visible ici :
https://raw.githubusercontent.com/iero/Kindle-weather-station/master/README.JPG

Basé sur le travail de Matthew Petroff (http://mpetroff.net/2012/09/kindle-weather-display/) mais adapté et francisé.

Utilise :
- Forecast.io python library - https://github.com/ZeevG/python-forecast.io
- Pngcrush - http://pmt.sourceforge.net/pngcrush/
- Request python library - http://docs.python-requests.org/en/latest/
- Modified netatmo python api - https://github.com/philippelt/netatmo-api-python
- Les icones de Noah Blon - http://codepen.io/noahblon/details/lxukH

Vous avez donc besoin d’une API Netatmo et d’une API foecast.io

Sur le raspberry (ou equivalent) :
- installer un serveur web (cf google)
- créer un répertoire kindle
- Compiler pngcrush (un binaire est gracieusement fourni)
- Copier les scripts du répertoire raspberry
- Modifier settings.xml
- Modifier la derniere ligne de weather-script.sh pour copier le fichier sur le serveur web. 
- Ajouter dans le cron (crontab -e) la ligne :
*/5 * * * * /home/pi/kindle/weather-script.sh

Sur le Kindle :

- Jailbreaker le Kindle. Pour le Kindle 4, j’ai utilisé cette page : http://wiki.mobileread.com/wiki/Kindle4NTHacking
- Installer USBNetwork pour activer le ssh http://www.mobileread.com/forums/showthread.php?t=88004
- Installer Kual et activer le ssh via wifi http://www.mobileread.com/forums/showthread.php?t=203326

- Modifier kindle/display-weather pour mettre l’addresse du raspberry
- Mettre les fichiers du répertoire kindle dans /mnt/us/weather/
- Lancer le cron toutes les 5 minutes (décallées de 2 minutes) pour mettre à jour la page

kindle# /mnt/us/kindle/init-weather.sh
kindle# mntroot rw
kindle# echo « */5+2 * * * * /mnt/us/weather/display-weather.sh » >> /etc/crontab/root
kindle# mntroot ro
kindle# /etc/init.d/cron restart