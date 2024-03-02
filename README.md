# ZERO TOUCH AUTOMATION SOFTWARE PREVENTING SECURITY VULNERABILITY
# Emrah UZDILLI- CI/CD Pipilene using DEVSECOPS......
# Trigger Test...
![Mind map](https://github.com/emrah-uzdilli/DevSecOps-WebApplication/assets/62702253/5abe489e-38e1-410d-a2bf-ccf6d6d308e8)

# DevSecOps provides automation from the beginning of a process that reduces the
# chance of any mistakes, which can lead to vulnerabilities. The DevSecOps motto is;
# “Software,safer,sooner”.

# The CI/CD pipeline is designed to streamline software development and deployment making it more
# efficient, automated and secure.

![image](https://github.com/emrah-uzdilli/DevSecOps-WebApplication/assets/62702253/97eb8a70-f3be-4fe6-a51d-cc076f878f15)

# In Jenkins there are 2 pipeline, which listen to all the time Development branch at Git-Hub with
# WebHook integration. Whenever arrives new commit AutomationVulnuribilities_CI pipeline
# triggered automatically and start do analysis of vulnerabilities at GitHub Repositories, Docker Images
# and Dependencies.

![image](https://github.com/emrah-uzdilli/DevSecOps-WebApplication/assets/62702253/1bc0b394-25f1-4786-a38a-94afbd3b647a)

# Trivy Docker Image Vulnerabilities Analysis
Trivy utilizes the National Vulnerability Database (NVD) and other reliable sources to maintain a
collection of Common Vulnerabilities and Exposures (CVEs). This collection is regularly updated to
ensure that Trivy can effectively detect vulnerabilities. The generated report offers an overview of
these vulnerabilities providing details, about the impacted packages and their severity levels. The
report includes a list of vulnerabilities accompanied by their CVE IDs, severity levels well as
additional resources for further understanding. To integrate Trivy into your CI/CD pipelines you
would need to incorporate it into your development and deployment workflows to conduct scans,
on container images.
![image](https://github.com/emrah-uzdilli/DevSecOps-WebApplication/assets/62702253/06fcd615-148f-4276-894f-4c8176dbfd1e)

# Trivy Repository Vulnerabilities Analysis
When we discuss scanning repositories, on GitHub we are essentially referring to the act of
inspecting the source code and project files within a GitHub repository. The objective is to pinpoint
elements such as security vulnerabilities, issues with code quality and adherence, to practices. This
practice holds importance in ensuring that software projects hosted on GitHub are dependable,
secure and simple to manage.
![image](https://github.com/emrah-uzdilli/DevSecOps-WebApplication/assets/62702253/9ac21bae-0b56-449b-a7db-04456e239c15)
