This repository contains document templates and supporting code for generating
individualized official lab result reports for SARS-CoV-2 / hCoV-19 / COVID-19
tests performed by Northwest Genomics Center.

Requirements:

  * XeLaTeX
  * TeX Live
  * Droid package from TeX Live, if you don't have the full distribution
  * Python 3.6+
    - latex
    - jinja2

You can install the Python dependencies with pip:

    python3 -m pip install -r requirements.txt

Since TeX Live has a somewhat onerous installation process, a Docker image may
be built containing all the dependencies required to run the report generation.

To build the image:

    make docker

To use it to run `fill-template`, for example:

    docker run --rm lab-result-reports ./fill-template scan/report-en.tex > report.pdf

Note that the image is entirely self-contained and includes a copy of this
repository; the `./fill-template` and `scan/report-en.tex` above refer to those
"baked into" image.

If you're using the image during development of the templates or code, make
sure to run `make docker` after every change to update the image.  You can also
overlay your local, active source dir into the container at `/src`:

    docker run --rm -v $PWD:/src lab-result-reports ./fill-template scan/report-en.tex > report.pdf

The image is not yet pushed to Docker Hub.
