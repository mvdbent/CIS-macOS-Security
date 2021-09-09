# CIS-macOS-Security Compliance Project
<img src="https://github.com/mvdbent/CIS-macOS-Security/blob/main/custom/Images/CIS-macOS-Security.png" width="250">

_**Current state of the scripts are:** "This project is 'As is" please be free to give me any feedback_

![GitHub](https://img.shields.io/badge/macOS-11-success)
![GitHub](https://img.shields.io/github/license/mvdbent/CIS-macOS-Security)

## DESCRIPTION
This CIS Benchmark rule set is build to use with the macOS Security Compliance Project [here](https://github.com/usnistgov/macos_security)

## Info
While working with CIS Benchmarks PDF (guidelines for scripts and/or Configuration Profiles) I felt there must be a better and faster way. The guys from the macOS Security Compliance Project did an amazing job automating the guidance, needed scripts, configuration profiles, and remediation script.

So I started to transform the CIS Benchmark PDF from Big Sur into custom rules set to integrate with the macOS Security Compliance Project.

## Usage/Requirements
*The CIS Benchmark rules are tested on macOS Big Sur 11.* and the latest macOS Security Compliance Project release.*

1. Download the **CIS-macOS-Security** to your device. 
2. Download the **macOS Security Compliance Project** to your device.
3. Install the Prerequisites for the **macOS Security Compliance Project**, see instuctions [here](https://github.com/usnistgov/macos_security/wiki/Getting-Started)
4. Copy the **CIS-macOS-Security** `/custom/` folder into the **macOS Security Compliance Project** and overwrite the empty `/custom/` folder. 

The `/custom/` folder in the **macOS Security Compliance Project** is in the .gitignore file so you can safely update to the latest version of **macOS Security Compliance Project** without loosing the **CIS Benchmark baselines**.


### Generate a Baseline
The project provides the following baseline files, located in the `/custom/baselines/` folder:

* CIS-Benchmark.yaml
* CIS-Benchmark-L1.yaml
* CIS-Benchmark-L2.yaml

If you want to create your own baseline or modify an existing baseline, the `generate-baseline.py` found in the scripts folder will generate a `{baseline}.yaml` file containing all the rules corresponding with the provided tag (baseline). This `{baseline}.yaml` is required to run the `generate-guidance.py` script.

Get a list of available tags and you will see the CIS-Benchmark tags as well
```bash
$ macOS-Security git:(master) ./scripts/generate_baseline.py -l
```

* 800-171
* 800-53r4_high
* 800-53r4_low
* 800-53r4_moderate
* **CIS-Benchmark**
* **CIS-Benchmark-L1**
* **CIS-Benchmark-L2**
* cnssi-1253
* inherent
* manual
* n_a
* none
* permanent
* stig
* supplemental

**Generate a new baseline**

```bash
$ macOS-Security git:(master) ./scripts/generate_baseline.py -k CIS-Benchmark-L1
$ macOS-Security git:(master) ls -dn build/baselines/*
-rw-r--r--  1 501  20  6350 May 10 13:30 build/baselines/CIS-Benchmark-L1.yaml
```
The generated baseline will be saved into the `build/baselines/`

### Generate CIS Benchmark guidance

To generate the guidance files (AsciiDoc, HTML, PDF, Excel, mobileconfigs, and compliance script) run the `generate-guidance.py` script and point it to either one of the built-in `baseline.yaml` files or a custom CIS Benchmark baseline.yaml file in the `custom/baselines` folder or created by the `generate-baseline.py` script.

**AsciiDoc, HTML, and PDF**

```bash
$ ./scripts/generate_guidance.py custom/baselines/CIS-Benchmark.yaml
```

**AsciiDoc, HTML, and PDF with custom logo **

```bash
$ ./scripts/generate_guidance.py custom/baselines/CIS-Benchmark.yaml -l /Git/macOS-Security/custom/Images/cis_banner.png
```

**AsciiDoc, HTML, PDF, and Excel**

```bash
$ ./scripts/generate_guidance.py custom/baselines/CIS-Benchmark.yaml -x
```
**AsciiDoc, HTML, PDF, Excel, and mobileconfigs**

```bash
$ ./scripts/generate_guidance.py custom/baselines/CIS-Benchmark.yaml -x -p
```

**AsciiDoc, HTML, PDF, Excel, mobileconfigs, and custom logo**
_use full-path to custom logo_
```bash
$ ./scripts/generate_guidance.py custom/baselines/CIS-Benchmark.yaml -l /Git/macOS-Security/custom/Images/cis_banner.png -p -x
```
