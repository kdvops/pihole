# pihole



## get password from manifest
kubectl -n pihole exec -it pod/<pihole-pod-name> -- \
  cat /etc/pihole/setupVars.conf | grep WEBPASSWORD



## Reset Password
kubectl -n pihole exec -it pod/<pihole-pod-name> -- \
  pihole -a -p



### getpassword from secret
kubectl -n pihole get secret pihole-webpassword -o yaml

kubectl -n pihole get secret pihole-webpassword \
  -o jsonpath='{.data.WEBPASSWORD}' | base64 --decode



####
Usar DNS upstream custom:
unbound.pihole.svc.cluster.local#5335



#####

##probar consulta DNS
kubectl exec -n pihole -it <pihole-pod> -- dig google.com
