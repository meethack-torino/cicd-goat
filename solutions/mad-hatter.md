[![CICD-SEC-4 Poisoned Pipeline Execution (PPE)](https://img.shields.io/badge/CICD--SEC--4-Poisoned%20Pipeline%20Execution%20(PPE)-brightgreen)](https://github.com/OWASP/www-project-top-10-ci-cd-security-risks/blob/main/CICD-SEC-04-Poisoned-Pipeline-Execution.md)

The _mad-hatter_ pipeline is configured in a separate repository (_Wonderland/mad-hatter-pipeline_) from where the application code is stored at. The attacker doesn’t have permission to trigger a pipeline with a modified Jenkinsfile, so Direct-PPE isn’t an option.

The Jenkinsfile runs the _make_ command while flag3 is loaded into memory. Execute an [Indirect-PPE](https://github.com/OWASP/www-project-top-10-ci-cd-security-risks/blob/main/CICD-SEC-04-Poisoned-Pipeline-Execution.md) attack by modifying the Makefile and exfiltrate the flag.



1. Modify the Makefile in the main branch under the _Wonderland/mad-hatter_ repository to print _flag3_ to the console output of the Jenkins job (or send it to a host you control).


    ```Makefile
    whoami:
        echo "${FLAG}" | base64
    ```



2. A pipeline will be triggered automatically. Access the console output of the executed job to get the encoded secret.
![mad_hatter](../images/mad_hatter.png "mad_hatter")