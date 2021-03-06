.. _no-std-ru:

==================================
Сборка с использованием ``no_std``
==================================

В этом руководстве показано, как включить ``no_std`` для вашего смарт-контракта rust,
потенциально уменьшая размер результирующего модуля Wasm на несколько килобайт.

Подготовка
===========

Компиляция ``concordium-std`` без ``std`` требует использования набора rust инструментов
nightly toolchain, который можно установить с помощью ``rustup``:

.. code-block:: console

   $rustup toolchain install nightly

Настройка модуля для ``no_std``
===============================

Библиотека ``concordium-std`` предоставляет ``std``, который позволяет
использовать стандартную библиотеку rust.
Эта функция включена по умолчанию.

Чтобы отключить это, нужно просто отключить функции по умолчанию для
``concordium-std`` в зависимостях вашего модуля.

.. code-block:: rust

   [dependencies]
   concordium-std = { version: "=0.2", default-features = false }

Чтобы иметь возможность переключаться между использованием std и без std, также добавьте ``std``
в свой собственный модуль, который включает функцию ``std`` в ``concordium-std``:

.. code-block:: rust

   [features]
   std = ["concordium-std/std"]

Это пример настройки смарт-контрактов, где ``std`` для каждого
модуля смарт-контракта включен по умолчанию.

Сборка модуля
===================

Чтобы использовать набор инструментов nightly toolchain, добавьте ``+nightly``
сразу после ``cargo``:

.. code-block:: console

   $cargo +nightly concordium build

Если вы хотите отключить функции по умолчанию вашего собственного модуля
смарт-контракта, вы можете передать дополнительные аргументы для ``cargo``:

.. code-block:: console

   $cargo +nightly concordium build -- --no-default-features
