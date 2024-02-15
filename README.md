# challenge-s15-e02


## Exercice 1: HorizontalPodAutoScaler

Créez un deployment démarrant l'image Nginx à l'image du challenge-s15-e01
Ce deployment aura un replica : 1
Attention à limiter au maximum vos requests et limits de vos containers


Créez un Horizontal Pod AutoScaler qui pointera sur ce deployment, précisant un nombre de pods minimums de 2.
Observez le nombre de pods présents dans votre namespace.


## Exercice 2: InitContainers
Help: https://kubernetes.io/docs/concepts/workloads/pods/init-containers/

Creez une configmap comprenant à minima la clevaleur suivante:
firstname: votreprenom
Ajoutez plus de contenu à votre convenance

Modifiez votre deployment pour charger toutes la configmap comme variable d'environnement.

Modifiez votre deployment pour y ajouter un initContainer, cet initContainer affichera le contenu de la 
variable d'environnement $firstname provenant de la configmap dans un echo.
Cet initContainer utilisera l'image busybox et vous devrez impérativement surcharger la commande de démarrage du container.


## Exercice 3: initContainers + PVC

Modifiez le deployment de l'exercice 2 pour que votre deployment définisse un volume basé sur un PVC.
Exemple de PVC:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: gp2-claim-1
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: gp2
  resources:
    requests:
      storage: 1Gi

```

L'initContainer montera ce PVC dans /data

Modifiez l'initContainer celui ci ajoutera une ligne dans /data/myfile avec le contenu de la variable firstname ainsi que la date.
Il affichera ensuite le contenu du fichier:

echo $firstname >> /data/myfile
date >> /data/myfile
cat /data/myfile

Supprimez votre pod à plusieurs reprises et consultez les logs du container initContainer de votre Pod.
https://kubernetes.io/docs/tasks/debug/debug-application/debug-init-containers/


