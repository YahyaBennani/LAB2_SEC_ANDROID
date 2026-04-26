# LAB2_SEC_ANDROID
<img width="1266" height="512" alt="root" src="https://github.com/user-attachments/assets/a3cf65cc-5a9a-43de-8f08-0122fb999ea4" />


# Rapport d’Audit – Lab 2 : Rooting Android & Analyse des Impacts

---

## 1. Périmètre

- **Application :** UnCrackable Level 1  
- **Environnement :** AVD (Android 36.1, Google APIs x86_64)  
- **Objectif :** Étudier le rooting, analyser ses impacts sécurité et observer les mécanismes de détection de root  
- **Données :** Fictives (lab)  
- **Réseau :** Environnement isolé (sandbox)

---

## 2. Rooting Android

Le rooting permet d’obtenir les privilèges administrateur (root) sur Android.  
Cela offre un contrôle total du système, utile pour :

- Analyse avancée des applications
- Accès aux fichiers internes
- Contournement de protections

 **Risque :** suppression des mécanismes de sécurité (sandbox, isolation).  
 Nécessite : environnement isolé + reset après test.

---

## 3. Sécurité Android & Verified Boot

###  Principes de sécurité
- **Sandboxing :** isolation des apps  
- **Permissions :** accès contrôlé aux ressources  
- **Intégrité système :** vérifiée au démarrage  

###  Chaîne de confiance (AVB)


Hardware → Bootloader → Kernel → Système Android



- Chaque étape vérifie la suivante (signature)
- Protection contre modifications et rollback

---

## 4. Risques & Mesures

| Risques | Contre-mesures |
|--------|---------------|
| Résultats faussés | Logs + traçabilité |
| Surface d’attaque élevée | AVD dédié |
| Exposition de données | Données fictives |
| Instabilité système | APK limité |
| Fuite d’infos perso | Aucun compte réel |
| Persistance des données | Reset AVD |
| Réseau non isolé | Sandbox |
| Manque de traçabilité | Captures + logs |

---

## 5. Tests OWASP Mobile

###  MASVS
- **STORAGE-1 :** données sensibles chiffrées  
- **NETWORK-1 :** communications via TLS  

###  MASTG (Tests)
- **Détection Root :**
  - Recherche de `su`, Magisk, test-keys
  - Bypass possible (ex: Frida)

- **Analyse dynamique :**
  - `adb logcat`
  - Recherche de fuites d’informations

---

## 6. Observations

- **ADB :** appareil détecté  
- **Root :** confirmé (`uid=0`)  
- **Verified Boot :** état `orange` (système modifié)

###  Tests réalisés

1. **Lancement app**
   - Détection root → message "Root detected"

2. **Entrée utilisateur**
   - Rejet des chaînes incorrectes

3. **Analyse fichiers**
   - Accès à `/data/data/...` via root

---

## 7. Limites

- Protection anti-root active  
- Analyse dynamique limitée sans bypass  
- Nécessité d’outils avancés :
  - Frida (hooking)
  - Bypass des protections

---

