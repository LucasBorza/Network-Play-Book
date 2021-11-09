## Lumen to Masergy MPLS flip

The purpose of this script is to flip MPLS providers from the Lumen primary path to the Masergy backup path.

SSH into SITE.MPLS.MY (10.XX.10.12)

Apply the following commands:
```
router bgp [SITE-AS#]
no bgp default local-preference 50
no neighbor [MASERGY-PE-IP-ADDRESS] route-map PREPEND out
end
clear ip bgp * soft
!
```

SSH into SITE.MPLS.CL (10.XX.10.11)

Apply the following commands:
```
route-map PREPEND permit 10
set as-path prepend [SITE-AS#] [SITE-AS#] [SITE-AS#]
router bgp [SITE-AS#]
bgp default local-preference 50
neighbor [LUMEN-PE-IP-ADDRESS] route-map PREPEND out
end
clear ip bgp * soft
!
```