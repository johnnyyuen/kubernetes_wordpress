# kubernetes_wordpress

The files started with new_ means the nfs is directly configured in each deployment without setting up the NFS persistence volume

yet, still need to check when the port is not exposed by the load balancer



Wireguard
  - sudo su -
  - mkdir /etc/wireguard
  - wg genkey > /etc/wireguard/private
  - sudo ip link add wg0 type wireguard
  - sudo ip addr add 10.10.0.1/24 dev wg0
  - sudo wg set wg0 prinvate-key ./private
  - sudo wg set wg0 private-key ./private
  - ip link set wg0 up
  - sudo ip link set wg0 up
  - wg (get the public key)
  - tee wg.conf <<EOF
  [Interface]
  ListenPort = 37499
  PrivateKey = <privatekey>
  Address = 10.10.0.1/24

  [Peer]
  PublicKey = <publickey>
  AllowedIPs = 10.10.0.2/32
  Endpoint = 10.0.0.122:52006
  EOF
  
  systemctl enable wg-quick@wg0
  systemctl start wg-quick@wg0

  
