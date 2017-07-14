#################
Model
#################

.. in this section we are using the https://yuml.me/ service to generate UML diagrams on the fly providing the description of the diagram in the URL directly. We split the URL in different lines to improve the readability

The Benchmarking Suite is designed to be very generic and extensible. The main concept is the **BenchmarkExecution** that is the execution of a **Benchmark** in one **ExecutionEnvironment** provided by a **ServiceProvider**.

With this concepts, it is easy to model, for instance, the execution of the *YCSB* benchmark on a *Virtual Machine* provided by *Amazon AWS*.

.. image:: https://yuml.me/diagram/scruffy;dir:TB/class/
                [ExecutionEnvironment]0..*-1[ServiceProvider],
                [BenchmarkingExecution]0..*-1[Benchmark],
                [BenchmarkingExecution]1..*-1[ExecutionEnvironment]
    :align: center

Since it is frequent to execute multiple tests against the same Service Provider, the Benchmarking Suite has the concept of **BenchmarkingSession**. that can include one or more executions of the same provider.

.. image:: https://yuml.me/diagram/scruffy;dir:TB/class/[BenchmarkingSession]-1..*[BenchmarkingExecution],[BenchmarkingSession]-1[ServiceProvider],[BenchmarkingExecution]-[ExecutionEnvironment],[ExecutionEnvironment]-1[ServiceProvider].png
    :align: center

By default, all the executions of the same session share the same **ExecutionEnvironment**.