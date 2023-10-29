- Partimos de ubuntu 20.04
- https://certbot.eff.org/
  sudo snap install --classic certbot
- verificar que funciona $sudo certbot renew --dry-run
- sudo certbot --nginx --hsts --staple-ocsp --must-staple \
  -d sagibus.eu -d www.sagibux.eu
-
-
-