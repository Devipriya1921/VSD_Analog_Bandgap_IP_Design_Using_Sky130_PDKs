# VSD_Analog_Bandgap_IP_Design_Using_Sky130_PDKs

![image](https://user-images.githubusercontent.com/80625515/138239041-24971c6d-a864-47be-9bf5-1d2d2a1e4b9c.png)

## Table of Contents 
- [Workshop Contents](#workshop-contents)
- [Introduction](#introduction)
- [Types of BGR](#Types-of-BGR)
- [Self-Biased Current Mirror Based BGR](#Self-Biased-Current-Mirror-Based-BGR)
- [CTAT Voltage Generation Circuit](#CTAT-voltage-generation-circuit)
- [PTAT Voltage Generation Circuit](#PTAT-voltage-generation-circuit)
- [Design of Resistance R1](#Design-of-Resistance-R1)
- [Self-bias Current Mirror](#Self-bias-Current-Mirror)
- [Design of R2 Resistance](#Design-of-R2-Resistance)
- [Start-up Circuit](#Start-up-Circuit)
- [Bandgap Reference Circuit](#Bandgap-Reference-Circuit)
- [Final BGR](#Final-BGR)
- [Tools Used for Analog Design Flow](#Tools-Used-for-Analog-Design-Flow)
- [Schematic designs](#Schematic-designs)
- [ Pre-Layout Simulations](# Pre-Layout-Simulations)
- [Layout](#Layout)
- [References](#References)
- [Acknowledgement](#acknowledgement)
- [Author](#author)



## Workshop Contents

Analog Bandgap IP Design using 130nm PDKs :

- Day 1 

![contents](https://user-images.githubusercontent.com/83152452/138582699-be4fea86-c8c7-4a06-935b-f4226503fb80.png)

- Day 2 

![contents](https://user-images.githubusercontent.com/83152452/138582701-5cc1cfa7-4143-4ee7-92cb-7875a13830a0.png)

## Introduction

![intro](https://user-images.githubusercontent.com/83152452/138582938-5012a782-217b-4fb7-8857-f7801421852a.png)

![BGR1](https://user-images.githubusercontent.com/83152452/138582933-e5516f3b-3880-499e-b365-1bc872736e36.png)


![bgrcontent](https://user-images.githubusercontent.com/83152452/138582935-69d12eb4-1416-4772-b75b-fdc508f01f40.png)


#### Why BGR?

1. A battery is unsuitable for use as a reference voltage source.
  
2. A typical power supply is also not suitable.
    
3. A voltage reference IC used buried Zener Diode.
    
4. A Bandgap reference that can be integrated into bulk CMOS, Bi-CMOS, or Bipolar technologies without the use of external components.

#### Applications of BGR

1. Low dropout reglators (LDO)
2. DC-to-DC buck converters
3. Analog-to-Digital Converter (ADC)
4. Digital-to-Analog Converter (DAC)

![Screenshot from 2021-10-21 09-29-39](https://user-images.githubusercontent.com/80625515/138239732-8cd44bbd-610a-4ef4-847a-5a2aff7a2e3e.png)
![Screenshot from 2021-10-21 09-30-07](https://user-images.githubusercontent.com/80625515/138239917-b399727b-f27a-4bf2-878d-3bd0d8fddaff.png)


## Types of BGR

![bgrtypes](https://user-images.githubusercontent.com/83152452/138583106-472f5c50-d91f-4793-8f14-37491b779570.png)

## Self-Biased Current Mirror Based BGR

![BGR](https://user-images.githubusercontent.com/83152452/138583122-d8e799aa-f365-4b4b-b4bf-b5dccdc5b61b.png)

### Advantages

- Simplest topology
- Easy to design
- Always stable

### Limitations

- Low power supply rejection ratio (PSRR)
- Cascode design needed to reduce PSRR
- Voltage head-room issue
- Need start-up circuit


### BGR Components

![BGR_Principle](https://user-images.githubusercontent.com/83152452/138583154-efff0b0a-eb04-443e-bc31-be7cd376d095.png)

It has the following components : 

- CTAT voltage generation circuit
- PTAT voltage generation circuit
- Self-biased current mirror circuit
- Reference branch circuit
- Start-up circuit

## CTAT Voltage Generation Circuit

![CTAT](https://user-images.githubusercontent.com/83152452/138583276-d370890a-050b-4f6b-9a6a-068b26eb5e76.png)


## PTAT Voltage Generation Circuit

![PTAT](https://user-images.githubusercontent.com/83152452/138583280-a60acb62-a65c-4010-9a5f-4de1e750880b.png)


## Design of Resistance R1

- Resistance value can be calculated by the formula R1=VT ln(N)/I
- For 10uA current and N=8, R1=5.4k ohms

## Self-bias Current Mirror

### Current Mirror 

![currentmirror](https://user-images.githubusercontent.com/83152452/138583386-4a7e4108-139b-4585-8219-c83f437c7a02.png)

#### Objective of reference generation is to establish DC voltage or current,

- Independent of supply
- Independent of process and
- Well-defined behavior with temperature

#### Issues

- Iout=K * Iref hence can support any amount of current
- To define a current one more constraint to be added

#### Reference Branch

![refbranch1](https://user-images.githubusercontent.com/83152452/138583588-b5ff5823-cbc8-4399-b5de-34cdd515dab6.png)


## Design of R2 Resistance 

- Tempco. of Vref should be zero
- As all the values known, alpha can be calculated easily.
- R2 = alpha(R1)


## Start-up Circuit

![startup](https://user-images.githubusercontent.com/83152452/138583602-b17e4a67-5fad-4b95-a408-6a2e61335ff0.png)

- If the channel length modulation is negligible, the current hardly depends on the supply voltage.
- The main issue in supply independent biasing is the existence of degenerate bias points.
- There are two stable operating points
    - Iin = Iout = 0A (undesired operating point)
    - desired operating points
- Must keep the circuit out of the undesired point when the supply is turned on.
- Must not interface with the circuit once it reaches the desired operating point.


## Bandgap Reference Circuit

![fullbgr](https://user-images.githubusercontent.com/83152452/138583632-49012b03-897c-43fa-a494-ac3334915ca6.png)

## Final BGR

![finalbgr](https://user-images.githubusercontent.com/83152452/138583634-2e4c74fc-c8a3-441b-b328-b2c09f964d2f.png)

### Equations

![PTATEQN](https://user-images.githubusercontent.com/83152452/138583638-c3409107-f7d7-4681-afaf-d0424d2b7715.png)


## Tools Used for Analog Design Flow

![tools used](https://user-images.githubusercontent.com/83152452/138583687-e1e8b39a-0853-4c35-a148-bee1ed3f7689.png)

## Schematic designs

### CTAT Voltage Generation Circuit

```
**** ctat voltage generation circuit *****

.lib "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130.lib.spice" tt
.include "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130_fd_pr__model__pnp.model.spice"

.global vdd gnd
.temp 27

*** bjt definition
xqp1	gnd	gnd	qp1	gnd	sky130_fd_pr__pnp_05v5_W3p40L3p40	m=1

*** supply voltage and current
vsup	vdd	gnd	dc	2
isup	vdd	qp1	dc 	10u
.dc	temp	-40	125	5

*** control statement
.control
run
plot v(qp1)
.endc
.end
```

### PTAT Voltage Generation Circuit

```
**** ptat voltage generation circuit *****

.lib "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130.lib.spice tt"
.include "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130_fd_pr__model__pnp.model.spice"

.global vdd gnd
.temp 27

*** vcvs definition
e1	net2	gnd	ra1	qp1	gain=1000
xmp1    q1	net2   	vdd	vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=4
xmp2    q2    	net2    vdd     vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=4
	
*** bjt definition
xqp1	gnd	gnd	qp1	vdd	sky130_fd_pr__pnp_05v5_W3p40L3p40	m=1
xqp2    gnd     gnd     qp2     vdd     sky130_fd_pr__pnp_05v5_W3p40L3p40       m=8

*** high-poly resistance definition
xra1    ra1     na1     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  	l=7.8
xra2    na1     na2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41	l=7.8
xra3    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41	l=7.8
xra4    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41	l=7.8

*** voltage sources for current measurement
vid1	q1	qp1	dc	0
vid2	q2	ra1	dc	0

*** supply voltage
vsup	vdd	gnd	dc 	2
.dc	temp	-40	125	5

*** control statement
.control
run
plot v(qp1) v(ra1) v(qp2) v(net2)
plot vid1#branch vid2#branch
.endc
.end
```

### Resistor Bank Circuit

```
**** RES tempco circuit *****

.lib "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130.lib.spice tt"
.include "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130_fd_pr__model__pnp.model.spice"

.global vdd gnd
.temp 27

*** resistor definition
xra1    ra1     na1     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra2    na1     na2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra3    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra4    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8

*** supply current
vsup	vdd	gnd	dc	2
vid     qp2     gnd     dc      0
isup	gnd	ra1	dc 	10u
.dc	temp	-40	125	1	isup	1.25u	10u	1.25u

*** control statement
.control
run
plot v(ra1) 
plot v(ra1)/vid#branch
.endc
.end
```

### BGR Circuit

```
**** bandgap reference circuit using self-biase current mirror *****

.lib "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130.lib.spice tt"
.include "/home/adevipriya/cad_vsd/eda-technology/sky130/models/spice/models/sky130_fd_pr__model__pnp.model.spice"

.global vdd gnd
.temp 27

*** circuit definition ***

*** mosfet definitions self-biased current mirror and output branch
xmp1	net1	net2	vdd	vdd	sky130_fd_pr__pfet_01v8_lvt	l=2	w=5	m=4
xmp2    net2    net2    vdd     vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5    	m=4
xmp3    net3    net2    vdd     vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=4
xmn1    net1    net1    q1      gnd     sky130_fd_pr__nfet_01v8_lvt     l=1     w=5     m=8
xmn2    net2    net1    q2      gnd     sky130_fd_pr__nfet_01v8_lvt     l=1     w=5     m=8

*** start-upcircuit
xmp4    net4    net2    vdd     vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=1
xmp5    net5    net2    net4    vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=1
xmp6    net7    net6    net2    vdd     sky130_fd_pr__pfet_01v8_lvt     l=2     w=5     m=2
xmn3    net6    net6    net8    gnd     sky130_fd_pr__nfet_01v8_lvt     l=7     w=1     m=1
xmn4    net8    net8    gnd     gnd     sky130_fd_pr__nfet_01v8_lvt     l=7     w=1     m=1

*** bjt definition
xqp1	gnd	gnd	qp1	vdd	sky130_fd_pr__pnp_05v5_W3p40L3p40	m=1
xqp2    gnd     gnd     qp2     vdd     sky130_fd_pr__pnp_05v5_W3p40L3p40       m=8
xqp3    gnd     gnd     qp3     vdd     sky130_fd_pr__pnp_05v5_W3p40L3p40       m=1

*** high-poly resistance definition
xra1	ra1	na1	vdd	sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra2	na1     na2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra3    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xra4    na2     qp2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8

xrb1    vref    nb1     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb2    nb1     nb2     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb3    nb2     nb3     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb4    nb3     nb4     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb5    nb4     nb5     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb6    nb5     nb6     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb7    nb6     nb7     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb8    nb7     nb8     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb9    nb8     nb9     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb10   nb9     nb10    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb11   nb10    nb11    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb12   nb11    nb12    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb13   nb12    nb13    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb14   nb13    nb14    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb15   nb14    nb15    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb16   nb15    nb16    vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb17   nb16    qp3   	vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8
xrb18   nb16    qp3     vdd     sky130_fd_pr__res_high_po_1p41     w=1.41  l=7.8

*** voltage source for current measurement
vid1	q1	qp1	dc	0
vid2    q2      ra1     dc      0
vid3    net3    vref    dc      0
vid4    net7	net1	dc	0
vid5	net5	net6	dc	0

*** supply voltage
vsup	vdd	gnd	dc 	2
.dc	vsup	0	3.3	0.1
*.dc	temp	-40	125	5

*vsup	vdd	gnd	pulse	0	2	10n	1u	1u	1m	100u
*.tran	5n	10u

.control
run

plot v(vdd) v(net1) v(net2) v(qp1) v(ra1) v(qp2) v(vref) v(qp3)
plot vid1#branch vid2#branch vid3#branch vid4#branch vid5#branch

.endc
.end
```

## Pre-Layout Simulations

### CTAT Voltage Generation

#### Command

![ctat_voltage_gen-withmultiplebjt-command](https://user-images.githubusercontent.com/83152452/138583840-271296b3-2ff7-40ab-a5ea-4d431b3e6fd5.png)

#### Waveform

![ctat_voltage_gen-withmultiplebjt-wf](https://user-images.githubusercontent.com/83152452/138583848-5e74aa4d-8a73-4193-a85c-cc6aa4d3bfb0.png)

#### Command

![ctat_voltage_gen-command](https://user-images.githubusercontent.com/83152452/138583860-f4d8bb5f-3024-4b31-bb1f-a1e4a7a1ed68.png)

#### Waveform

![ctat_voltage_gen-wf](https://user-images.githubusercontent.com/83152452/138583863-0edabfa3-40a4-4715-b3cb-089289e2dcb0.png)

#### Command

![ctat_voltage_gen-var-current-command](https://user-images.githubusercontent.com/83152452/138583867-a985e30d-6aec-457a-bae1-463c958b4335.png)

#### Waveform

![ctat_voltage_gen-var-current-wf](https://user-images.githubusercontent.com/83152452/138583868-86de8642-b813-451f-a2f1-09a2df385ea1.png)


### PTAT Voltage Generation

#### Command

![ptat-vol-gen-ideal-current-source-command](https://user-images.githubusercontent.com/83152452/138583916-5234f861-5b22-4a1d-a9c2-39dc6bdc94c4.png)

#### Waveform

![ptat-vol-gen-ideal-current-source-wf](https://user-images.githubusercontent.com/83152452/138583922-0f0bd868-29ba-44ee-85db-6323a02cd355.png)

#### Command

![ptat-vol-gen-command](https://user-images.githubusercontent.com/83152452/138583933-c42b601a-0a46-4ff4-bafa-d2dcafe9f5fd.png)

#### Waveform

![ptat-vol-gen-wf-1](https://user-images.githubusercontent.com/83152452/138583937-f7e596fb-6934-493b-b865-0106f7eec4f6.png)

![ptat-vol-gen-wf-2](https://user-images.githubusercontent.com/83152452/138583940-e85285c0-a868-4d5e-a878-123da91d1ee6.png)


### Resistor Temperature Coefficient Measurement

#### Command & waveform

![res_tempco-command](https://user-images.githubusercontent.com/83152452/138584012-f5bb2d95-a60a-4428-81b9-5409d860506c.png)

#### Command

![res_tempco--varr-current-command](https://user-images.githubusercontent.com/83152452/138584013-dd7ac025-e58c-4847-bdcf-d2ee35475119.png)

#### Waveform

![res_tempco--varr-current-wf-1](https://user-images.githubusercontent.com/83152452/138584015-f3642e8a-e7d5-4676-bc07-4f800d3f9d08.png)

![res_tempco--varr-current-wf-2](https://user-images.githubusercontent.com/83152452/138584017-6071ed22-90ee-452e-ae48-2bba8423acdb.png)


## BGR Circuit

Command & Waveforms

![bgr-complete-cir-command](https://user-images.githubusercontent.com/83152452/138584065-c809ca76-59db-4a00-b517-af085ff9515f.png)

![bgr-complete-cir-wf-1](https://user-images.githubusercontent.com/83152452/138584068-aea9f0d5-e1ab-4640-95ea-2d60bcf3a0ff.png)

![bgr-complete-cir-wf-2](https://user-images.githubusercontent.com/83152452/138584071-9412649e-4cfb-4bd7-a109-fa62dc08a165.png)

![bgr-complete-cir-wf-3](https://user-images.githubusercontent.com/83152452/138584072-1c29e488-0d4d-42ac-a691-73d37c911a27.png)

![bgr-complete-cir-wf-4](https://user-images.githubusercontent.com/83152452/138584073-ae59fdb3-a0d6-49eb-ba24-509a13beb446.png)

![bgr-complete-cir-wf-5](https://user-images.githubusercontent.com/83152452/138584075-9af1de0e-5f49-4d45-bc04-7b5ce6b23014.png)

![bgr-complete-cir-wf-6](https://user-images.githubusercontent.com/83152452/138584077-126a724b-ce52-471e-809f-5d2cc5795003.png)

![bgr-complete-cir-wf-7](https://user-images.githubusercontent.com/83152452/138584080-cd6452d1-570d-4e6f-9721-db0ee93b03cd.png)

![bgr-complete-cir-wf-8](https://user-images.githubusercontent.com/83152452/138584083-ef8748f9-1a72-4065-afcc-794b9ece7c1d.png)

![bgr-complete-cir-wf-9](https://user-images.githubusercontent.com/83152452/138584098-c4a1966a-5bd7-46a8-af20-4e2ea9403acf.png)

![bgr-complete-cir-wf-10](https://user-images.githubusercontent.com/83152452/138584101-452faf62-c95b-41c7-ad64-d73f28b3b01a.png)


## Layout 


### BJTs

![magic-bjts-1](https://user-images.githubusercontent.com/83152452/138584173-5153027e-87ab-4aa4-913d-a27f78280c02.png)

![magic-bjts-2](https://user-images.githubusercontent.com/83152452/138584175-a2f3602a-aeea-48fd-a6cb-8b7dd43cfbe8.png)


### MOSFET(N-Channel)

![magic-mosfet-nfet-1](https://user-images.githubusercontent.com/83152452/138584198-ddd2240b-2035-40ec-948b-93f3b4bfc3b6.png)

![magic-mosfet-nfet-2](https://user-images.githubusercontent.com/83152452/138584200-b197e203-2a0a-4575-9ecc-06e6277bbb8a.png)

![magic-mosfet-nfet-3](https://user-images.githubusercontent.com/83152452/138584201-6ff6df2f-a355-4061-a4af-642cbe0a1edf.png)

![magic-mosfet-nfet-4](https://user-images.githubusercontent.com/83152452/138584202-75419455-c784-4388-970a-4c44386db0d9.png)


### MOSFET(N-Channel)

![magic-mosfet-pfet-1](https://user-images.githubusercontent.com/83152452/138584209-a87906b3-49b8-437a-8995-2986262883f5.png)

![magic-mosfet-pfet-2](https://user-images.githubusercontent.com/83152452/138584212-711dea21-7241-4664-a85c-93dd785fe317.png)


### Resistors

![magic-resistor-1](https://user-images.githubusercontent.com/83152452/138584224-0213709f-4873-4110-bfa5-a85b59b7f4d1.png)

![magic-resistor-2](https://user-images.githubusercontent.com/83152452/138584227-18aae7a1-b57a-45b3-8a95-da7fd5477fa0.png)


### BGR Layout

![magic-bgr-1](https://user-images.githubusercontent.com/83152452/138584246-1db8eda9-3d6a-4f00-b061-867d45fac6ed.png)

### Spice Extraction

![console win-magic](https://user-images.githubusercontent.com/83152452/138584247-229022de-a372-49d9-960a-ac7a06e9638b.png)

![nfet-spice-1](https://user-images.githubusercontent.com/83152452/138584249-49107a07-b405-415b-88a7-71c8e5aafbdd.png)

![nfet1-spice-1](https://user-images.githubusercontent.com/83152452/138584257-3b8ac0de-6689-4c6d-8ae6-a21f4b021ce0.png)


## References

- https://github.com/google/skywater-pdk
- https://github.com/vsdip/vsdopen2021_bgr


## Acknowledgement

- Kunal Ghosh, Co-founder, VSD, kunalpghosh@gmail.com
- Santunu Sarangi, Asst. Professor
- Anagha Ghosh, VSD


## Author

- A Devipriya, Bachelor of Engineering (ECE), Cambridge Institute of Technology, Bangalore, adevipriya1900@gmail.com






