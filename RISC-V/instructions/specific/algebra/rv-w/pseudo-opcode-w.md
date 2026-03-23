```
$pseudo_op rv_w::wl1re8.v vl1r.v 31..29=0 28=0 27..26=0 25=1 24..20=0x08 rs1 14..12=0x0 vd  6..0=0x07
$pseudo_op rv_w::wl2re8.v vl2r.v 31..29=1 28=0 27..26=0 25=1 24..20=0x08 rs1 14..12=0x0 vd  6..0=0x07
$pseudo_op rv_w::wl4re8.v vl4r.v 31..29=3 28=0 27..26=0 25=1 24..20=0x08 rs1 14..12=0x0 vd  6..0=0x07
$pseudo_op rv_w::wl8re8.v vl8r.v 31..29=7 28=0 27..26=0 25=1 24..20=0x08 rs1 14..12=0x0 vd  6..0=0x07

$pseudo_op rv_w::wlm.v vle1.v  31..28=0 27..26=0 25=1 24..20=0xb rs1 14..12=0x0  vd 6..0=0x07
$pseudo_op rv_w::wsm.v vse1.v  31..28=0 27..26=0 25=1 24..20=0xb rs1 14..12=0x0 vs3 6..0=0x27

$pseudo_op rv_w::wfredusum.vs  vfredsum.vs 31..26=0x01 vm vs2 vs1 14..12=0x1 vd 6..0=0x57
$pseudo_op rv_w::wfwredusum.vs vfwredsum.vs 31..26=0x31 vm vs2 vs1 14..12=0x1 vd 6..0=0x57

$pseudo_op rv_w::wcpop.m vpopc.m  31..26=0x10 vm vs2 19..15=0x10 14..12=0x2 rd 6..0=0x57

$pseudo_op rv_w::wmorn.mm  vmornot.mm 31..26=0x1c vm vs2 vs1 14..12=0x2 vd 6..0=0x57
$pseudo_op rv_w::wmandn.mm vmandnot.mm  31..26=0x18 vm vs2 vs1 14..12=0x2 vd 6..0=0x57
```
