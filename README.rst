.. image:: https://api.codeclimate.com/v1/badges/66560126d66fb438a9d4/maintainability
   :target: https://codeclimate.com/github/scivision/raspicam-raw-bayer/maintainability
   :alt: Maintainability

======================
raspicam-raw-bayer
======================
Acquire RAW Bayer-masked images with Raspberry Pi camera (before demosaicking).
Writes HDF5, NetCDF or TIFF compressed image stacks.

:author: Michael Hirsch, Ph.D.

.. contents::

Install
=======
To be installed directly on the Raspberry Pi, using Python >= 3.5::

    pip3 install -e .

To avoid MMAL errors, ``raspi-config`` > Advanced Options > Memory Split should be 128 MB, not 64 MB.

Examples
========

Setting of exposure time manually (seconds) is mandatory to avoid mistakes in experiments.

RAW live video display
----------------------
::

    ./getrawimage.py 0.01 -a

Dump image stack to disk
------------------------
NetCDF::

    ./getrawimage.py 0.01 output.nc

HDF5::

    ./getrawimage.py 0.01 output.h5

TIFF::

    ./getrawimage.py 0.01 output.tif


Command-Line Options
====================

-a            GPU-based preview, for aiming camera (fast)
-p            use Matplotlib for slow, live (10 seconds per frame) display
-e exp_sec    manually set exposure time, up to one second (TODO there are still some auto-set gains)
-8            output 8-bit array instead of default 10-bit array

Reference
========

`Constraints on exposure time <http://picamera.readthedocs.io/en/latest/fov.html#camera-modes>`_


Notes
=====

    ValueError: cannot save to a group with the scipy.io.netcdf backend

is because of missing::

    apt install libnetcdf-dev

    pip install netcdf4
