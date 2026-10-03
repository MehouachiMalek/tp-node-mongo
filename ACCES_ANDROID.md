# 8.2 Joindre l'API depuis un appareil mobile

| Client | URL de base |
|---|---|
| Postman / navigateur PC | http://localhost:5000/api/ |
| Émulateur Android | http://10.0.2.2:5000/api/ |
| Téléphone réel (iPhone 14 Pro Max, via partage de connexion) | http://172.20.10.6:5000/api/ |

## Étapes réalisées
1. IP du PC trouvée avec `ipconfig` : Adresse IPv4 = 172.20.10.6.
2. Accès autorisé à Node.js dans le pare-feu Windows.
3. Test de http://172.20.10.6:5000/api/health dans Safari sur iPhone.

## Résultat
La page affiche {"status":"ok"} (voir captures/health.jpeg).

## À retenir pour la séance Retrofit
- Ajouter la permission INTERNET dans AndroidManifest.xml.
- Créer res/xml/network_security_config.xml listant 10.0.2.2 et l'IP du PC.
- Déclarer ce fichier dans <application android:networkSecurityConfig="@xml/network_security_config">.