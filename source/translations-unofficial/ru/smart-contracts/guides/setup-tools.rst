.. _setup-tools-ru:

=====================================
Установка инструментов для разработки
=====================================

Прежде чем мы сможем начать разработку смарт-контрактов, нам нужно настроить
среду.

Rust и Cargo
============

Во-первых, `установите rustup`_, который установит Rust_ и Cargo_ на вашу
машину.
Затем используйте ``rustup`` для установки Wasm, которая используется для компиляции:

.. code-block:: console

   $rustup target add wasm32-unknown-unknown

Cargo Concordium
================

Cargo Concordium - это инструмент для разработки смарт-контрактов для блокчейна
Concordium.
Он может быть использован для :ref:`компиляции <compile-module-ru>` и
:ref:`тестирования <unit-test-contract-ru>` смарт-контрактов, и включает такие функции,
как :ref:`построение схемы контракта<build-schema-ru>`.

.. todo::

   Добавить ссылки для тестирования и схемы.

Cargo Concordium поставляется как часть пакета :ref:`программного обеспечения Concordium <downloads>`.
Инструмент должен быть помещен в ваш PATH.

Для описания того, как использовать Cargo Concordium, выполните:

.. code-block:: console

   $cargo concordium --help

Программное обеспечение Concordium
==================================

Инструмент для развертывания и взаимодействия со смарт-контрактами -
:ref:`concordium-клиент <concordium_client>`. Он распространяется как
часть пакета :ref:`программного обеспечения Concordium<downloads>`.

.. note::

   Чтобы развернуть модули смарт-контрактов и взаимодействовать с сетью,
   убедитесь, что вы :ref:`запустили ноду <run-a-node>`.

.. _Rust: https://www.rust-lang.org/
.. _Cargo: https://doc.rust-lang.org/cargo/
.. _установите rustup: https://rustup.rs/
.. _crates.io: https://crates.io/
