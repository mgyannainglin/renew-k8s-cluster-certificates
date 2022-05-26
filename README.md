# renew-kube-api-server-cert

1. Login with ssh into **master** node.
2. Double check **certificates** are expired or not.
    ```
        kubeadm certs check-expiration
    ```
    or
    ```
        kubeadm alpha certs check-expiration
    ```
    ![certificates are expired](\images\certs-expired.png)

3. Renew the certificate.

    ```
     kubeadm certs renew all
    ```

    ![certificates renew](.\images\renew-certs.png)

4. backup the old kubelet config and init the new config with new certs.

    1. 
    ```
        cd /etc/kubernetes/
    ```

    2. 

    ```
        mv kubelet.conf kubelet.conf.bk
    ```

    3. 

    ```
    kubeadm init phase kubeconfig kubelet
    ```

    4. 

    ```
    service kubelet restart
    ```

    5. 
    ```
    service kubelet status
    ```
    6. 

    ```
    reboot
    ```
    7. 
    ```
    cp /etc/kubernetes/kubelet.conf .kube/config 
    ```

Repeat all the step from ***stpe-1*** if you have two or more master nodes.
