1.13.2
------

*   Revert dask_worker to use fork rather than subprocess by default
*   Scatter retains type information
*   Bokeh always uses subprocess rather than spawn

1.13.1
------

*   Fix critical Windows error with dask_worker executable

1.13.0
------

*   Rename Executor to Client #492
*   Add `--memory-limit` option to `dask-worker`, enabling spill-to-disk
    behavior when running out of memory #485
*   Add `--pid-file` option to dask-worker and `--dask-scheduler` #496
*   Add ``upload_environment`` function to distribute conda environments.
    This is experimental, undocumented, and may change without notice.  # 494
*   Add `workers=` keyword argument to `Client.compute` and `Client.persist`,
    supporting location-restricted workloads with Dask collections #484
*   Add ``upload_environment`` function to distribute conda environments.
    This is experimental, undocumented, and may change without notice.  # 494
    *   Add optional `dask_worker=` keyword to `client.run` functions that gets
        provided the worker or nanny object
    *   Add `nanny=False` keyword to `Client.run`, allowing for the execution
        of arbitrary functions on the nannies as well as normal workers


1.12.2
------

This release adds some new features and removes dead code

*   Publish and share datasets on the scheduler between many clients
    https://github.com/dask/distributed/pull/453
    http://distributed.readthedocs.io/en/latest/publish.html
*   Launch tasks from other tasks (experimental)
    https://distributed.readthedocs.io/en/latest/task-launch.html
    https://github.com/dask/distributed/pull/471
*   Remove unused code, notably the `Center` object and older client functions
    https://github.com/dask/distributed/pull/478
*   Executor() and LocalCluster() is now robust to Bokeh's absence
    https://github.com/dask/distributed/pull/481
*   Removed s3fs and boto3 from requirements.  These have moved to Dask.

1.12.1
------

This release is largely a bugfix release, recovering from the previous large
refactor.

*  Fixes from previous refactor
    *  Ensure idempotence across clients
    *  Stress test losing scattered data permanently
*  IPython fixes
    *  Add `start_ipython_scheduler` method to Executor
    *  Add `%remote` magic for workers
    *  Clean up code and tests
*  Pool connects to maintain reuse and reduce number of open file handles
*  Re-implement work stealing algorithm
*  Support cancellation of tuple keys, such as occur in dask.arrays
*  Start synchronizing against worker data that may be superfluous
*  Improve bokeh plots styling
    *  Add memory plot tracking number of bytes
    *  Make the progress bars more compact and align colors
    *  Add workers/ page with workers table, stacks/processing plot, and memory
*  Add this release notes document


1.12.0
------

This release was largely a refactoring release.  Internals were changed
significantly without many new features.

*  Major refactor of the scheduler to use transitions system
*  Tweak protocol to traverse down complex messages in search of large
   bytestrings
*  Add dask-submit and dask-remote
*  Refactor HDFS writing to align with changes in the dask library
*  Executor reconnects to scheduler on broken connection or failed scheduler
*  Support sklearn.external.joblib as well as normal joblib
