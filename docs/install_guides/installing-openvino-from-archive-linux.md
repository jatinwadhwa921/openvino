# Install OpenVINO™ Runtime on Linux from an Archive File {#openvino_docs_install_guides_installing_openvino_from_archive_linux}

With the OpenVINO™ 2022.3 release, you can download and use archive files to install OpenVINO Runtime. The archive files contain pre-built binaries and library files needed for OpenVINO Runtime, as well as code samples.

Installing OpenVINO Runtime from archive files is recommended for C++ developers. If you are working with Python, the PyPI package has everything needed for Python development and deployment on CPU and GPUs. See the [Install OpenVINO from PyPI](installing-openvino-pip.md) page for instructions on how to install OpenVINO Runtime for Python using PyPI.

> **NOTE**: Since the OpenVINO™ 2022.1 release, the following development tools: Model Optimizer, Post-Training Optimization Tool, Model Downloader and other Open Model Zoo tools, Accuracy Checker, and Annotation Converter can be installed via [pypi.org](https://pypi.org/project/openvino-dev/2022.3.1/) only.

See the [Release Notes](https://www.intel.com/content/www/us/en/developer/articles/release-notes/openvino-2022-3-lts-relnotes.html) for more information on updates in the latest release.


@sphinxdirective

.. tab:: System Requirements

  | Full requirement listing is available in:
  | `System Requirements Page <https://www.intel.com/content/www/us/en/developer/tools/openvino-toolkit/system-requirements.html>`__

.. tab:: Processor Notes

  Processor graphics are not included in all processors.
  See `Product Specifications`_ for information about your processor.

  .. _Product Specifications: https://ark.intel.com/

.. tab:: Software

  * `CMake 3.13 or higher, 64-bit <https://cmake.org/download/>`__
  * `Python 3.7 - 3.10, 64-bit <https://www.python.org/downloads/>`__
  * GCC:

  .. tab:: Ubuntu 18.04

    * GCC 7.5.0

  .. tab:: Ubuntu 20.04

    * GCC 9.3.0

  .. tab:: RHEL 8

    * GCC 8.4.1

  .. tab:: CENTOS 7

    * GCC 8.3.1
    Use folloving instructions to install it:
    Install GCC 8.3.1 via devtoolset-8

    .. code-block:: sh

      sudo yum update -y && sudo yum install -y centos-release-scl epel-release
      sudo yum install -y devtoolset-8 git patchelf

    Enable devtoolset-8 and check current gcc version

    .. code-block:: sh

      source /opt/rh/devtoolset-8/enable
      gcc -v

@endsphinxdirective

## Installing OpenVINO Runtime

### <a name="install-openvino-archive-linux"></a>Step 1: Download and Install the OpenVINO Core Components

@sphinxdirective

1. Open a command prompt terminal window. You can use the keyboard shortcut: Ctrl+Alt+T

2. Create the ``/opt/intel`` folder for OpenVINO by using the following command. If the folder already exists, skip this step.

   .. code-block:: sh

      sudo mkdir /opt/intel

   .. note::
      The ``/opt/intel`` path is the recommended folder path for administrators or root users. If you prefer to install OpenVINO in regular userspace, the recommended path is ``/home/<USER>/intel``. You may use a different path if desired.

3. Browse to the current user's ``Downloads`` folder:

   .. code-block:: sh

      cd <user_home>/Downloads

4. Download the `OpenVINO Runtime archive file for your system <https://storage.openvinotoolkit.org/repositories/openvino/packages/2022.3.1/linux/>`__, extract the files, rename the extracted folder and move it to the desired path:

   .. tab:: Ubuntu 20.04

      .. code-block:: sh

         curl -L https://storage.openvinotoolkit.org/repositories/openvino/packages/2022.3.1/linux/l_openvino_toolkit_ubuntu20_2022.3.1.9227.cf2c7da5689_x86_64.tgz --output openvino_2022.3.1.tgz
         tar -xf openvino_2022.3.1.tgz
         sudo mv l_openvino_toolkit_ubuntu20_2022.3.1.9227.cf2c7da5689_x86_64 /opt/intel/openvino_2022.3.1

   .. tab:: Ubuntu 18.04

      .. code-block:: sh

         curl -L https://storage.openvinotoolkit.org/repositories/openvino/packages/2022.3.1/linux/l_openvino_toolkit_ubuntu18_2022.3.1.9227.cf2c7da5689_x86_64.tgz --output openvino_2022.3.1.tgz
         tar -xf openvino_2022.3.1.tgz
         sudo mv l_openvino_toolkit_ubuntu18_2022.3.1.9227.cf2c7da5689_x86_64 /opt/intel/openvino_2022.3.1

   .. tab:: RHEL 8

      .. code-block:: sh

         curl -L https://storage.openvinotoolkit.org/repositories/openvino/packages/2022.3.1/linux/l_openvino_toolkit_rhel8_2022.3.1.9227.cf2c7da5689_x86_64.tgz --output openvino_2022.3.1.tgz
         tar -xf openvino_2022.3.1.tgz
         sudo mv l_openvino_toolkit_rhel8_2022.3.1.9227.cf2c7da5689_x86_64 /opt/intel/openvino_2022.3.1

   .. tab:: CentOS 7

      .. code-block:: sh

         curl -L https://storage.openvinotoolkit.org/repositories/openvino/packages/2022.3.1/linux/l_openvino_toolkit_centos7_2022.3.1.9227.cf2c7da5689_x86_64.tgz --output openvino_2022.3.1.tgz
         tar -xf openvino_2022.3.1.tgz
         sudo mv l_openvino_toolkit_centos7_2022.3.1.9227.cf2c7da5689_x86_64 /opt/intel/openvino_2022.3.1

5. Install required system dependencies on Linux. To do this, OpenVINO provides a script in the extracted installation directory. Run the following command:

   .. code-block:: sh

      cd /opt/intel/openvino_2022.3.1
      sudo -E ./install_dependencies/install_openvino_dependencies.sh

6. (Optional) Install *numpy* Python Library:

   .. note::

      This step is required only when you decide to use Python API.

   You can use the ``requirements.txt`` file from the ``/opt/intel/openvino_2022.3.1/python/python.<x>`` folder:

   .. code-block:: sh

      cd /opt/intel/openvino_2022.3.1
      python3 -m pip install -r ./python/python3.<x>/requirements.txt

7. For simplicity, it is useful to create a symbolic link as below:

   .. code-block:: sh

      cd /opt/intel
      sudo ln -s openvino_2022.3.1 openvino_2022

   .. note::
      If you have already installed a previous release of OpenVINO 2022, a symbolic link to the ``openvino_2022`` folder may already exist. Unlink the previous link with ``sudo unlink openvino_2022``, and then re-run the command above.

@endsphinxdirective

Congratulations, you finished the installation! The `/opt/intel/openvino_2022` folder now contains the core components for OpenVINO. If you used a different path in Step 2, for example, `/home/<USER>/Intel/`, OpenVINO is then installed in `/home/<USER>/Intel/openvino_2022`. The path to the `openvino_2022` directory is also referred as `<INSTALL_DIR>` throughout the OpenVINO documentation.

### <a name="set-the-environment-variables-linux"></a>Step 2: Configure the Environment

You must update several environment variables before you can compile and run OpenVINO applications. Open a terminal window and run the `setupvars.sh` script as shown below to temporarily set your environment variables. If your <INSTALL_DIR> is not `/opt/intel/openvino_2022`, use the correct one instead.

```sh
source /opt/intel/openvino_2022/setupvars.sh
```  

If you have more than one OpenVINO version on your machine, you can easily switch its version by sourcing the `setupvars.sh` of your choice.

> **NOTE**: The above command must be re-run every time you start a new terminal session. To set up Linux to automatically run the command every time a new terminal is opened, open `~/.bashrc` in your favorite editor and add `source /opt/intel/openvino_2022/setupvars.sh` after the last line. Next time when you open a terminal, you will see `[setupvars.sh] OpenVINO™ environment initialized`. Changing `.bashrc` is not recommended when you have multiple OpenVINO versions on your machine and want to switch among them.

The environment variables are set. Continue to the next section if you want to download any additional components.

### <a name="model-optimizer-linux">Step 3 (Optional): Install Additional Components
OpenVINO Development Tools is a set of utilities for working with OpenVINO and OpenVINO models. It provides tools like Model Optimizer, Benchmark Tool, Post-Training Optimization Tool, and Open Model Zoo Downloader. If you install OpenVINO Runtime using archive files, OpenVINO Development Tools must be installed separately.

See the [Install OpenVINO Development Tools](installing-model-dev-tools.md) page for step-by-step installation instructions.

OpenCV is necessary to run demos from Open Model Zoo (OMZ). Some OpenVINO samples can also extend their capabilities when compiled with OpenCV as a dependency. To install OpenCV for OpenVINO, see the [instructions on GitHub](https://github.com/opencv/opencv/wiki/BuildOpenCV4OpenVINO).

### <a name="optional-steps-linux"></a>Step 4 (Optional): Configure Inference on Non-CPU Devices
OpenVINO Runtime has a plugin architecture that enables you to run inference on multiple devices without rewriting your code. Supported devices include integrated GPUs, discrete GPUs, NCS2, VPUs, and GNAs. See the instructions below to set up OpenVINO on these devices.

@sphinxdirective
.. tab:: GPU

   To enable the toolkit components to use processor graphics (GPU) on your system, follow the steps in :ref:`GPU Setup Guide <gpu guide>`.

.. tab:: NCS 2

   To perform inference on Intel® Neural Compute Stick 2 powered by the Intel® Movidius™ Myriad™ X VPU, follow the steps on :ref:`NCS2 Setup Guide <ncs guide>`.
   <!--For more details, see the `Get Started page for Intel® Neural Compute Stick 2 <https://software.intel.com/en-us/neural-compute-stick/get-started>`.-->

.. tab:: VPU

   To install and configure your Intel® Vision Accelerator Design with Intel® Movidius™ VPUs, see the :ref:`VPU Configuration Guide <vpu guide>`.
   After configuration is done, you are ready to run the verification scripts with the HDDL Plugin for your Intel® Vision Accelerator Design with Intel® Movidius™ VPUs.

   .. warning::
      While working with either HDDL or NCS, choose one of them as they cannot run simultaneously on the same machine.

.. tab:: GNA

   To enable the toolkit components to use Intel® Gaussian & Neural Accelerator (GNA) on your system, follow the steps in :ref:`GNA Setup Guide <gna guide>`.

@endsphinxdirective

## <a name="get-started-linux"></a>What's Next?
Now that you've installed OpenVINO Runtime, you're ready to run your own machine learning applications! Learn more about how to integrate a model in OpenVINO applications by trying out the following tutorials.

@sphinxdirective
.. tab:: Get started with Python

   Try the `Python Quick Start Example <https://docs.openvino.ai/2022.3/notebooks/201-vision-monodepth-with-output.html>`_ to estimate depth in a scene using an OpenVINO monodepth model in a Jupyter Notebook inside your web browser.

   .. image:: https://user-images.githubusercontent.com/15709723/127752390-f6aa371f-31b5-4846-84b9-18dd4f662406.gif
      :width: 400

   Visit the :ref:`Tutorials <notebook tutorials>` page for more Jupyter Notebooks to get you started with OpenVINO, such as:

   * `OpenVINO Python API Tutorial <https://docs.openvino.ai/2022.3/notebooks/002-openvino-api-with-output.html>`_
   * `Basic image classification program with Hello Image Classification <https://docs.openvino.ai/2022.3/notebooks/001-hello-world-with-output.html>`_
   * `Convert a PyTorch model and use it for image background removal <https://docs.openvino.ai/2022.3/notebooks/205-vision-background-removal-with-output.html>`_

.. tab:: Get started with C++

   Try the `C++ Quick Start Example <openvino_docs_get_started_get_started_demos.html>`_ for step-by-step instructions on building and running a basic image classification C++ application.

   .. image:: https://user-images.githubusercontent.com/36741649/127170593-86976dc3-e5e4-40be-b0a6-206379cd7df5.jpg
      :width: 400

   Visit the :ref:`Samples <code samples>` page for other C++ example applications to get you started with OpenVINO, such as:

   * `Basic object detection with the Hello Reshape SSD C++ sample <openvino_inference_engine_samples_hello_reshape_ssd_README.html>`_
   * `Automatic speech recognition C++ sample <openvino_inference_engine_samples_speech_sample_README.html>`_

@endsphinxdirective

## <a name="uninstall-from-linux"></a>Uninstalling the Intel® Distribution of OpenVINO™ Toolkit

To uninstall the toolkit, follow the steps on the [Uninstalling page](uninstalling-openvino.md).

## Additional Resources

@sphinxdirective

* :ref:`Troubleshooting Guide for OpenVINO Installation & Configuration <troubleshooting guide for install>`
* Converting models for use with OpenVINO™: :ref:`Model Optimizer User Guide <deep learning model optimizer>`
* Writing your own OpenVINO™ applications: :ref:`OpenVINO™ Runtime User Guide <deep learning openvino runtime>`
* Sample applications: :ref:`OpenVINO™ Toolkit Samples Overview <code samples>`
* Pre-trained deep learning models: :ref:`Overview of OpenVINO™ Toolkit Pre-Trained Models <model zoo>`
* IoT libraries and code samples in the GitHub repository: `Intel® IoT Developer Kit`_

.. _Intel® IoT Developer Kit: https://github.com/intel-iot-devkit

@endsphinxdirective

## Additional Resources

- [OpenVINO Installation Selector Tool](https://www.intel.com/content/www/us/en/developer/tools/openvino-toolkit/download.html)