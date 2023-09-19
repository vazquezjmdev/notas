- kubectl get pods -l app=mailhog
  kubectl exec -it deployment/mailhog -- sh
  kubectl get pods -l app=mailhog -o  jsonpath="{.items[*].status.containerStatuses[*].containerID}"
-
-