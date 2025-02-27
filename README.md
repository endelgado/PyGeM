  <p align="center">
  <a href="http://mathlab.github.io/PyGeM/" target="_blank" >
    <img alt="Python Geometrical Morphing" src="docs/source/_static/logo_PyGeM.png" width="200" />
  </a>
</p>
<p align="center">
    <a href="LICENSE.rst" target="_blank">
        <img alt="Software License" src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square">
    </a>
    <a href="https://travis-ci.org/mathLab/PyGeM" target="_blank">
        <img alt="Build Status" src="https://travis-ci.org/mathLab/PyGeM.svg">
    </a>
    <a href="https://coveralls.io/github/mathLab/PyGeM?branch=master" target="_blank">
        <img alt="Coverage Status" src="https://coveralls.io/repos/github/mathLab/PyGeM/badge.svg?branch=master">
    </a>
    <a href="https://www.codacy.com/app/mathLab/PyGeM?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=mathLab/PyGeM&amp;utm_campaign=Badge_Grade" target="_blank">
        <img alt="Codacy Badge" src="https://api.codacy.com/project/badge/Grade/7299abd9d61c4aa586903d80cea01c82">
    </a>
</p>

[PyGeM](http://mathlab.github.io/PyGeM/) (Python Geometrical Morphing) is a python package that allows you to deform a given geometry or mesh with different deformation techniques such as FFD, RBF and IDW.

## Table of contents
* [Description](#description)
* [Dependencies and installation](#dependencies-and-installation)
	* [Docker](#docker)
* [Documentation](#documentation)
* [Testing](#testing)
* [Examples](#examples)
* [How to cite](#how-to-cite)
	* [References](#references)
	* [Recent works with PyGeM](#recent-works-with-pygem)
* [Authors and contributors](#authors-and-contributors)
* [How to contribute](#how-to-contribute)
* [License](#license)

## Description
**PyGeM** is a python package using **Free Form Deformation**, **Radial Basis Functions** and **Inverse Distance Weighting** to parametrize and morph complex geometries.  It is ideally suited for actual industrial problems, since it allows to handle:

- Computer Aided Design files (in .iges, .step, and .stl formats)
- Mesh files (in .unv and OpenFOAM formats)
- Output files (in .vtk format)
- LS-Dyna Keyword files (.k format)

By now, it has been used with meshes with up to 14 milions of cells. Try with more and more complicated input files! 
See the [**Examples**](#examples) section below and the [**Tutorials**](tutorials/README.md) to have an idea of the potential of this package.


## Dependencies and installation
**PyGeM** requires `numpy`, `scipy`, `matplotlib`, `vtk`, `numpy-stl`, `sphinx` (for the documentation) and `nose` (for local test). They can be easily installed via `pip`. The code is compatible with Python 2.7 and Python 3.6.
Moreover **PyGeM** depends on `OCC`. These requirements cannot be satisfied through `pip`.
Please see the table below for instructions on how to satisfy the `OCC` requirements. You can also refer to `pythonocc.org` or `github.com/tpaviot/pythonocc-core` for further instructions.

| Package | Version     | How to install (precompiled binaries via conda)                                                          |
|---------|-------------|----------------------------------------------------------------------------------------------------------|
| OCC     | ==0.17.3    | Python2.7 `conda install -c conda-forge -c dlr-sc -c pythonocc -c oce pythonocc-core==0.17 python=2.7` |
| OCC     | ==0.17.3    | Python3.6 `conda install -c conda-forge -c dlr-sc -c pythonocc -c oce pythonocc-core==0.17 python=3.6` |


The official distribution is on GitHub, and you can clone the repository using

```bash
> git clone https://github.com/mathLab/PyGeM
```

To install the package just type:

```bash
> python setup.py install
```

To uninstall the package you have to rerun the installation and record the installed files in order to remove them:

```bash
> python setup.py install --record installed_files.txt
> cat installed_files.txt | xargs rm -rf
```

### Docker
Alternatively, a way to run the PyGeM library is to use our prebuilt and high-performance Docker images.
Docker containers are extremely lightweight, secure, and are based on open standards that run on all major Linux distributions, macOS and Microsoft Windows platforms.

Install Docker for your platform by following [these instructions](https://docs.docker.com/engine/getstarted/step_one/).
If using the Docker Toolbox (macOS versions < 10.10 or Windows versions < 10), make sure you run all commands inside the Docker Quickstart Terminal.

Now we will pull the docker.io/pygemdocker/pygem image from our cloud infrastructure:
```bash
>  docker pull docker.io/pygemdocker/pygem:latest
```
Docker will pull the latest tag of the image pygemdocker/pygem from docker.io. The download is around 3.246 GB. The  image is a great place to start experimenting with PyGeM and includes all dependencies already compiled for you.
Once the download is complete you can start PyGeM for the first time. Just run:
```bash
>  docker run -ti  pygemdocker/pygem:latest
```
To facilitate the devoloping, using the text editor,version control and other tools already installed on your computers,
it is possible to share files from the host into the container:

```bash
>  docker run -ti -v $(pwd):/home/PyGeM/shared  pygemdocker/pygem:latest
```
To allow the X11 forwarding in the container, on Linux system just run:

```bash
>  docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v $(pwd):/home/PyGeM/shared  pygemdocker/pygem:latest
```

For Windows system, you need to install Cygwin/X version and running the command in Cygwin terminal. While for mac system, you need to install xquartz. 

## Documentation
**PyGeM** uses [Sphinx](http://www.sphinx-doc.org/en/stable/) for code documentation. You can view the documentation online [here](http://mathlab.github.io/PyGeM/). To build the html versions of the docs locally simply:

```bash
> cd docs
> make html
```

The generated html can be found in `docs/build/html`. Open up the `index.html` you find there to browse.


## Testing
We are using Travis CI for continuous intergration testing. You can check out the current status [here](https://travis-ci.org/mathLab/PyGeM).

To run tests locally (the package `nose` is required):

```bash
> python test.py
```


## Examples
You can find useful tutorials on how to use the package in the [tutorials](tutorials/README.md) folder.
Here we show three applications, taken from the **naval**, **nautical** and **automotive** engineering fields. On the other hand, the provided tutorials are related to easier geometries.
<p align="center">
<img src="readme/DTMB_ffd.png" alt>
</p>
<p align="center">
<em>DTMB-5415 hull: morphing of the bulbous bow starting from an industrial .iges CAD file.</em>
</p>

<p align="center">
<img src="readme/scafoYZshift.gif" alt>
</p>
<p align="center">
<em>MCY hull: morphing of the exhaust gasses devices starting from an industrial .stl file.</em>
</p>

<p align="center">
<img src="readme/drivAer_ffd.png" alt>
</p>
<p align="center">
<em>DrivAer model: morphing of the bumper starting from an OpenFOAM mesh file.</em>
</p>

## How to cite
If you use this package in your publications please cite the package as follows:

```tex
\bibitem{pygem}
{PyGeM: Python Geometrical Morphing. Available at}: \href{https://github.com/mathLab/PyGeM}{https://github.com/mathLab/PyGeM}.
```

### References
The deformations implemented are taken from the following papers:

* Sieger, Menzel, Botsch. *On Shape Deformation Techniques for Simulation-based Design Optimization*. SEMA SIMAI Springer Series, 2015. [[DOI](https://doi.org/10.1007/978-3-319-06053-8_14)], [[pdf](http://www.honda-ri.de/pubs/pdf/1052.pdf)],
[[bibitem](readme/sieger2015shape.bib)].

* Forti, Rozza. *Efficient geometrical parametrisation techniques of interfaces for reduced-order modelling: application to fluid–structure interaction coupling problems*. International Journal of Computational Fluid Dynamics, 2014. [[DOI](http://dx.doi.org/10.1080/10618562.2014.932352)],
[[bibitem](readme/forti2014efficient.bib)].

* Sieger, Menzel, Botsch. *RBF Morphing Techniques for Simulation-based Design Optimization*. M. Engineering with Computers, 2014. [[DOI](https://doi.org/10.1007/s00366-013-0330-1)], [[pdf](http://www.honda-ri.de/pubs/pdf/923.pdf)],
[[bibitem](readme/sieger2014rbf.bib)].

* Lombardi, Parolini, Quarteroni, Rozza. *Numerical Simulation of Sailing Boats: Dynamics, FSI, and Shape Optimization*. Springer Optimization and Its Applications, 2012. [[DOI](http://dx.doi.org/10.1007/978-1-4614-2435-2_15)], [[pdf](https://infoscience.epfl.ch/record/175879/files/PaerErice-Lombardi-parolini-quarteroni-Rozza.pdf)],
[[bibitem](readme/lombardi2012numerical.bib)].

### Recent works with PyGeM
Here there is a list of the scientific works involving **PyGeM** you can consult and/or cite. If you want to add one, please open a PR.

* Tezzele, Demo, Rozza. *Shape optimization through proper orthogonal decomposition with interpolation and dynamic mode decomposition enhanced by active subspaces*.In Proceedings of MARINE 2019: VIII International Conference on Computational Methods in Marine Engineering, pages 122-133, 2019.
[[DOI](https://congress.cimne.com/marine2019/frontal/Doc/EbookMarine2019.pdf)],
[[arXiv](https://arxiv.org/abs/1905.05483)],
[bibitem](readme/tezzele2019marine.bib)].

* Demo, Tezzele, Mola, Rozza. *A complete data-driven framework for the efficient solution of parametric shape design and optimisation in naval engineering problems*. In Proceedings of MARINE 2019: VIII International Conference on Computational Methods in Marine Engineering, pages 111-121, 2019. 
[[DOI](https://congress.cimne.com/marine2019/frontal/Doc/EbookMarine2019.pdf)],
[[arXiv](https://arxiv.org/abs/1905.05982)],
[bibitem](readme/demo2019marine.bib)].

* Tezzele, Demo, Mola, Rozza. *An integrated data-driven computational pipeline with model order reduction for industrial and applied mathematics*. Submitted, 2018. [[arXiv](https://arxiv.org/abs/1810.12364)],
[[bibitem](readme/tezzele2018ecmi.bib)].

* Tezzele, Salmoiraghi, Mola, Rozza. *Dimension reduction in heterogeneous parametric spaces with application to naval engineering shape design problems*. Advanced Modeling and Simulation in Engineering Sciences, 2018. [[DOI](https://doi.org/10.1186/s40323-018-0118-3)], [[arXiv](https://arxiv.org/abs/1709.03298)], [[bibitem](readme/tezzele2018dimension.bib)].

* Tezzele, Ballarin, Rozza. *Combined parameter and model reduction of cardiovascular problems by means of active subspaces and POD-Galerkin methods*. In Mathematical and Numerical Modeling of the Cardiovascular System and Applications. SEMA SIMAI Springer Series vol. 16, 2018. [[DOI](https://doi.org/10.1007/978-3-319-96649-6_8)], [[arXiv](https://arxiv.org/abs/1711.10884)],
[[bibitem](readme/tezzele2018combined.bib)]. 

* Salmoiraghi, Scardigli, Telib, Rozza. *Free-form deformation, mesh morphing and reduced-order methods: enablers for efficient aerodynamic shape optimisation*. International Journal of Computational Fluid Dynamics, 2018. [[DOI](https://doi.org/10.1080/10618562.2018.1514115)], [[arXiv](https://arxiv.org/abs/1803.04688)],
[[bibitem](readme/salmoiraghi2018free.bib)].

* Demo, Tezzele, Gustin, Lavini, Rozza. *Shape optimization by means of proper orthogonal decomposition and dynamic mode decomposition*. In Technology and Science for the Ships of the Future: Proceedings of NAV 2018: 19th International Conference on Ship & Maritime Research, 2018. [[DOI](https://doi.org/10.3233/978-1-61499-870-9-212)], [[arXiv](https://arxiv.org/abs/1803.07368)],
[[bibitem](readme/demo2018shape.bib)].

* Tezzele, Demo, Gadalla, Mola, Rozza. *Model Order Reduction by means of Active Subspaces and Dynamic Mode Decomposition for Parametric Hull Shape Design Hydrodynamics*. In Technology and Science for the Ships of the Future: Proceedings of NAV 2018: 19th International Conference on Ship & Maritime Research, 2018. [[DOI](https://doi.org/10.3233/978-1-61499-870-9-569)], [[arXiv](https://arxiv.org/abs/1803.07377)],
[[bibitem](readme/tezzele2018model.bib)].
 
* Demo, Tezzele, Mola, Rozza. *An efficient shape parametrisation by free-form deformation enhanced by active subspace for hull hydrodynamic ship design problems in open source environment*. The 28th International Ocean and Polar Engineering Conference, 2018. [[arXiv](https://arxiv.org/abs/1801.06369)],
[[bibitem](readme/demo2018isope.bib)].

* Bergmann, Ferrero, Iollo, Lombardi, Scardigli, Telib. *A zonal Galerkin-free POD model for incompressible flows*. Journal of Computational Physics, 2018. [[DOI](https://doi.org/10.1016/j.jcp.2017.10.001)],
[[bibitem](readme/bergmann2018zonal.bib)].

* Salmoiraghi, Ballarin, Corsi, Mola, Tezzele, Rozza. *Advances in geometrical parametrization and reduced order models and methods for computational fluid dynamics problems in applied sciences and engineering: overview and perspectives*. ECCOMAS 2016 proceedings. [[DOI](https://doi.org/10.7712/100016.1867.8680)],
[[bibitem](readme/salmoiraghi2016advances.bib)].


## Authors and contributors
**PyGeM** is currently developed and mantained at [SISSA mathLab](http://mathlab.sissa.it/) by
* [Marco Tezzele](mailto:marcotez@gmail.com)
* [Nicola Demo](mailto:demo.nicola@gmail.com)

under the supervision of [Prof. Gianluigi Rozza](mailto:gianluigi.rozza@sissa.it). We thank [Filippo Salmoiraghi](mailto:filippo.salmoiraghi@gmail.com) for the original idea behind this package and the major contributions.

Contact us by email for further information or questions about **PyGeM**, or suggest pull requests. Contributions improving either the code or the documentation are welcome!


## How to contribute
We'd love to accept your patches and contributions to this project. There are
just a few small guidelines you need to follow.

### Submitting a patch

  1. It's generally best to start by opening a new issue describing the bug or
     feature you're intending to fix.  Even if you think it's relatively minor,
     it's helpful to know what people are working on.  Mention in the initial
     issue that you are planning to work on that bug or feature so that it can
     be assigned to you.

  2. Follow the normal process of [forking][] the project, and setup a new
     branch to work in.  It's important that each group of changes be done in
     separate branches in order to ensure that a pull request only includes the
     commits related to that bug or feature.

  3. To ensure properly formatted code, please make sure to use 4
     spaces to indent the code. The easy way is to run on your bash the provided
     script: ./code_formatter.sh. You should also run [pylint][] over your code.
     It's not strictly necessary that your code be completely "lint-free",
     but this will help you find common style issues.

  4. Any significant changes should almost always be accompanied by tests.  The
     project already has good test coverage, so look at some of the existing
     tests if you're unsure how to go about it. We're using [coveralls][] that
     is an invaluable tools for seeing which parts of your code aren't being
     exercised by your tests.

  5. Do your best to have [well-formed commit messages][] for each change.
     This provides consistency throughout the project, and ensures that commit
     messages are able to be formatted properly by various git tools.

  6. Finally, push the commits to your fork and submit a [pull request][]. Please,
     remember to rebase properly in order to maintain a clean, linear git history.

[forking]: https://help.github.com/articles/fork-a-repo
[pylint]: https://www.pylint.org/
[coveralls]: https://coveralls.io
[well-formed commit messages]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[pull request]: https://help.github.com/articles/creating-a-pull-request


## License

See the [LICENSE](LICENSE.rst) file for license rights and limitations (MIT).
