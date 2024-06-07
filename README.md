<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![GNU GPL v3.0 License][license-shield]][license-url]
<!-- [![LinkedIn][linkedin-shield]][linkedin-url] -->



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <!-- <a href="https://github.com/fkemser/CUPSwrapper">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a> -->

<h3 align="center">CUPSwrapper</h3>

  <p align="center">
    A collection of shell scripts to interactively print and manage printers via command line.
    <br />
    <a href="https://github.com/fkemser/CUPSwrapper"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/fkemser/CUPSwrapper">View Demo</a>
    ·
    <a href="https://github.com/fkemser/CUPSwrapper/issues">Report Bug</a>
    ·
    <a href="https://github.com/fkemser/CUPSwrapper/issues">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
        <li><a href="#testing-environment">Testing Environment</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li>
          <a href="#prerequisites">Prerequisites</a>
          <ul>
            <li><a href="#alpine-linux">Alpine Linux</a></li>
            <li><a href="#debian">Debian</a></li>
          </ul>
        </li>
        <li>
          <a href="#os-settings">OS Settings</a>
          <ul>
            <li><a href="#windows-subsystem-for-linux-wsl-users-only">Windows Subsystem for Linux (WSL) Users Only</a></li>
          </ul>
        </li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage-srccupssh">Usage (/src/cups.sh)</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This project provides a `dialog`-based interface to

- set up a printer,  
![Screenshot 1][screenshot1]

- select a default printer,
- set default printing settings,
- print a document (or `stdin` input), allowing the user to interactively choose printer and printing settings,  
![Screenshot 2][screenshot2]

- create print job settings (`lp` arguments) that can be saved into a variable for multiple usage,  
![Screenshot 3][screenshot3]

- cancel print jobs.  
![Screenshot 4][screenshot4]

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Built With

[![Shell Script][Shell Script-shield]][Shell Script-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Testing Environment

The project has been developed and tested on the following system:

| Info | Description
---: | ---
OS | Debian GNU/Linux 12 (bookworm)
Kernel | 5.15.133.1-microsoft-standard-WSL2
Packages | [avahi-daemon (0.8-10)](https://packages.debian.org/bookworm/avahi-daemon)
|| [coreutils (9.1-1)](https://packages.debian.org/bookworm/coreutils)
|| [cups (2.4.2-3+deb12u5)](https://packages.debian.org/bookworm/cups)
|| [dash (0.5.12-2)](https://packages.debian.org/bookworm/dash)
|| [dialog (1.3-20230209-1)](https://packages.debian.org/bookworm/dialog)
|| [libc-bin (2.36-9+deb12u3)](https://packages.debian.org/bookworm/libc-bin)
|| [printer-driver-all (0.20210903)](https://packages.debian.org/bookworm/printer-driver-all)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

### Prerequisites
Please make sure that the following dependencies are installed:

* [Avahi](https://avahi.org/)
* [CUPS](https://openprinting.github.io/cups/)
* [Dialog](https://invisible-island.net/dialog/dialog.html)
* In case you have an older printer that does not support driverless printing (IPP) yet you may also need additional
legacy drivers.

Below you can find distribution-specific installation instructions.

#### Alpine Linux
```sh
# Required
echo "https://dl-cdn.alpinelinux.org/alpine/v$(cut -d'.' -f1,2 /etc/alpine-release)/community/" | sudo tee -a /etc/apk/repositories
echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing/" | sudo tee -a /etc/apk/repositories
sudo apk update
sudo apk add avahi cups cups-filters cups-pdf@testing dialog

# Optional
sudo apk add gutenprint-cups@testing
```

#### Debian
```sh
sudo apt install avahi-daemon cups dialog   # Required
sudo apt install printer-driver-all         # Optional
```

### OS Settings
The current user must be a member of the 'lpadmin' group:

```sh
sudo usermod -a -G lpadmin <username>
```

#### Windows Subsystem for Linux (WSL) Users Only
Please make sure that `systemd` is enabled as the default system/session manager. For more information please have a look at: https://learn.microsoft.com/en-us/windows/wsl/systemd

### Installation

1. Clone the repo
	```sh
   git clone --recurse-submodules https://github.com/fkemser/CUPSwrapper.git
   ```
2. Edit the repository configuration file. In case it is empty just keep it as it is, **do not delete it**.
	```sh
   nano ./CUPSwrapper/etc/cups.cfg.sh
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage (/src/cups.sh)

```sh
================================================================================
===============================     SYNOPSIS     ===============================
================================================================================

There are multiple ways to run this script:

Interactive mode (without any args):
> ./cups.sh

Classic (script) mode:
> ./cups.sh [ OPTION ]... ACTION [<file>]

ACTION := { -h|--help | --jobsettings | --print [<file>] }

[<file>] : File to print (optional)

--------------------------------------------------------------------------------
--------------------------------     ACTION     --------------------------------
--------------------------------------------------------------------------------

-h|--help            Show this help message                                     

--submenu <menu>     Run a certain submenu interactively and exit               
                                                                                
                     <menu> = { add | default | defsettings | remove | print }  

--jobsettings        Interactively select printer and print job settings. The   
                     chosen settings will be printed to <stdout>, e.g. for      
                     further use with 'lp' command.                             

--print [<file>]     Print, either from a given <file> or a previous command's  
                     output (via pipe). Interactively select printer and print  
                     job settings before printing.                              

================================================================================
===============================     EXAMPLES     ===============================
================================================================================

____________________________________ Print _____________________________________

./cups.sh --print letter.pdf     # Print a PDF file named 'letter.pdf'
echo Hello | ./cups.sh --print   # Print a command's output, here 'echo Hello'
```



<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/fkemser/CUPSwrapper/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the **GNU General Public License v3.0 (or later)**. See [`LICENSE`][license-url] for more information.

> :warning: The license above does not apply to the files and folders within the library directory `/lib`. Please have a look at the `LICENSE` file located in the root directory of each library to get more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Project Link: [https://github.com/fkemser/CUPSwrapper](https://github.com/fkemser/CUPSwrapper)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments
###
* [othneildrew/Best-README-Template](https://github.com/othneildrew/Best-README-Template)
* [Ileriayo/markdown-badges](https://github.com/Ileriayo/markdown-badges)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/fkemser/CUPSwrapper.svg?style=for-the-badge
[contributors-url]: https://github.com/fkemser/CUPSwrapper/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/fkemser/CUPSwrapper.svg?style=for-the-badge
[forks-url]: https://github.com/fkemser/CUPSwrapper/network/members
[stars-shield]: https://img.shields.io/github/stars/fkemser/CUPSwrapper.svg?style=for-the-badge
[stars-url]: https://github.com/fkemser/CUPSwrapper/stargazers
[issues-shield]: https://img.shields.io/github/issues/fkemser/CUPSwrapper.svg?style=for-the-badge
[issues-url]: https://github.com/fkemser/CUPSwrapper/issues
[license-shield]: https://img.shields.io/github/license/fkemser/CUPSwrapper.svg?style=for-the-badge
[license-url]: https://github.com/fkemser/CUPSwrapper/blob/master/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/linkedin_username

[screenshot1]: res/screenshot1.gif
[screenshot2]: res/screenshot2.gif
[screenshot3]: res/screenshot3.gif
[screenshot4]: res/screenshot4.gif

[LaTeX-shield]: https://img.shields.io/badge/latex-%23008080.svg?style=for-the-badge&logo=latex&logoColor=white
[LaTeX-url]: https://www.latex-project.org/
[Shell Script-shield]: https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white
[Shell Script-url]: https://pubs.opengroup.org/onlinepubs/9699919799/