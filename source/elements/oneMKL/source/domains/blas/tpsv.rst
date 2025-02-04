.. SPDX-FileCopyrightText: 2019-2020 Intel Corporation
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _onemkl_blas_tpsv:

tpsv
====

Solves a system of linear equations whose coefficients are in a
triangular packed matrix.

.. _onemkl_blas_tpsv_description:

.. rubric:: Description

The ``tpsv`` routines solve a system of linear equations whose
coefficients are in a triangular packed matrix. The operation is
defined as:

.. math::

      op(A)*x = b

where:

op(``A``) is one of op(``A``) = ``A``, or op(``A``) =
``A``\ :sup:`T`, or op(``A``) = ``A``\ :sup:`H`,

``A`` is an ``n``-by-``n`` unit or non-unit, upper or lower
triangular band matrix, supplied in packed form,

``b`` and ``x`` are vectors of length ``n``.

``tpsv`` supports the following precisions.

   .. list-table:: 
      :header-rows: 1

      * -  T 
      * -  ``float`` 
      * -  ``double`` 
      * -  ``std::complex<float>`` 
      * -  ``std::complex<double>`` 

.. _onemkl_blas_tpsv_buffer:

tpsv (Buffer Version)
---------------------

.. rubric:: Syntax
      
.. code-block:: cpp

   namespace oneapi::mkl::blas::column_major {
       void tpsv(sycl::queue &queue,
                 onemkl::uplo upper_lower,
                 onemkl::transpose trans,
                 onemkl::diag unit_nonunit,
                 std::int64_t n,
                 std::int64_t k,
                 sycl::buffer<T,1> &a,
                 sycl::buffer<T,1> &x,
                 std::int64_t incx)
   }
.. code-block:: cpp

   namespace oneapi::mkl::blas::row_major {
       void tpsv(sycl::queue &queue,
                 onemkl::uplo upper_lower,
                 onemkl::transpose trans,
                 onemkl::diag unit_nonunit,
                 std::int64_t n,
                 std::int64_t k,
                 sycl::buffer<T,1> &a,
                 sycl::buffer<T,1> &x,
                 std::int64_t incx)
   }

.. container:: section

   .. rubric:: Input Parameters

   queue
      The queue where the routine should be executed.

   upper_lower
      Specifies whether ``A`` is upper or lower triangular. See :ref:`onemkl_datatypes` for more details.

   trans
      Specifies op(``A``), the transposition operation applied to ``A``. See :ref:`onemkl_datatypes` for more details.

   unit_nonunit
      Specifies whether the matrix ``A`` is unit triangular or not. See :ref:`onemkl_datatypes` for more details.

   n
      Numbers of rows and columns of ``A``. Must be at least zero.

   a
      Buffer holding input matrix ``A``. Must have size at least
      (``n``\ \*(``n``\ +1))/2. See :ref:`matrix-storage` for
      more details.

   x
      Buffer holding the ``n``-element right-hand side vector ``b``. The
      buffer must be of size at least (1 + (``n`` - 1)*abs(``incx``)).
      See :ref:`matrix-storage` for
      more details.

   incx
      Stride of vector ``x``.

.. container:: section

   .. rubric:: Output Parameters

   x
      Buffer holding the solution vector ``x``.

.. container:: section

   .. rubric:: Throws

   This routine shall throw the following exceptions if the associated condition is detected. An implementation may throw additional implementation-specific exception(s) in case of error conditions not covered here.

   :ref:`oneapi::mkl::invalid_argument<onemkl_exception_invalid_argument>`
       
   
   :ref:`oneapi::mkl::unsupported_device<onemkl_exception_unsupported_device>`
       

   :ref:`oneapi::mkl::host_bad_alloc<onemkl_exception_host_bad_alloc>`
       

   :ref:`oneapi::mkl::device_bad_alloc<onemkl_exception_device_bad_alloc>`
       

   :ref:`oneapi::mkl::unimplemented<onemkl_exception_unimplemented>`
      

.. _onemkl_blas_tpsv_usm:

tpsv (USM Version)
------------------

.. rubric:: Syntax

.. code-block:: cpp

   namespace oneapi::mkl::blas::column_major {
       sycl::event tpsv(sycl::queue &queue,
                        onemkl::uplo upper_lower,
                        onemkl::transpose trans,
                        onemkl::diag unit_nonunit,
                        std::int64_t n,
                        std::int64_t k,
                        const T *a,
                        T *x,
                        std::int64_t incx,
                        const std::vector<sycl::event> &dependencies = {})
   }
.. code-block:: cpp

   namespace oneapi::mkl::blas::row_major {
       sycl::event tpsv(sycl::queue &queue,
                        onemkl::uplo upper_lower,
                        onemkl::transpose trans,
                        onemkl::diag unit_nonunit,
                        std::int64_t n,
                        std::int64_t k,
                        const T *a,
                        T *x,
                        std::int64_t incx,
                        const std::vector<sycl::event> &dependencies = {})
   }

.. container:: section

   .. rubric:: Input Parameters

   queue
      The queue where the routine should be executed.

   upper_lower
      Specifies whether ``A`` is upper or lower triangular. See :ref:`onemkl_datatypes` for more details.

   trans
      Specifies op(``A``), the transposition operation applied to
      ``A``. See :ref:`onemkl_datatypes` for more details.

   unit_nonunit
      Specifies whether the matrix ``A`` is unit triangular or not. See :ref:`onemkl_datatypes` for more details.

   n
      Numbers of rows and columns of ``A``. Must be at least zero.

   a
      Pointer to input matrix ``A``. The array holding input matrix
      ``A`` must have size at least (``n``\ \*(``n``\ +1))/2. See
      :ref:`matrix-storage` for
      more details.

   x
      Pointer to the ``n``-element right-hand side vector ``b``. The
      array holding the ``n``-element right-hand side vector ``b``
      must be of size at least (1 + (``n`` - 1)*abs(``incx``)). See
      :ref:`matrix-storage` for
      more details.

   incx
      Stride of vector ``x``.

   dependencies
      List of events to wait for before starting computation, if any.
      If omitted, defaults to no dependencies.

.. container:: section

   .. rubric:: Output Parameters

   x
      Pointer to the solution vector ``x``.

.. container:: section

   .. rubric:: Return Values

   Output event to wait on to ensure computation is complete.

.. container:: section

   .. rubric:: Throws

   This routine shall throw the following exceptions if the associated condition is detected. An implementation may throw additional implementation-specific exception(s) in case of error conditions not covered here.

   :ref:`oneapi::mkl::invalid_argument<onemkl_exception_invalid_argument>`
       
       
   
   :ref:`oneapi::mkl::unsupported_device<onemkl_exception_unsupported_device>`
       

   :ref:`oneapi::mkl::host_bad_alloc<onemkl_exception_host_bad_alloc>`
       

   :ref:`oneapi::mkl::device_bad_alloc<onemkl_exception_device_bad_alloc>`
       

   :ref:`oneapi::mkl::unimplemented<onemkl_exception_unimplemented>`
      

   **Parent topic:** :ref:`blas-level-2-routines`
