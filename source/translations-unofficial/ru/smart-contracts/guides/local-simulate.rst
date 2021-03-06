.. _local-simulate-ru:

=========================================
Локальное моделирование функций контракта
=========================================

Это руководство о том, как локально имитировать вызов некоторой init или
receive функции из модуля смарт-контракта Wasm в заданном контексте и
состоянии.
Это моделирование полезно для проверки смарт-контракта и его результатов в
конкретных сценариях.

.. seealso::

   Руководство по автоматическим модульным тестам см. :ref:`unit-test-contract-ru`.

Подготовка
===========

Убедитесь, что у вас установлен ``cargo-concordium``, если нет, следуйте руководству
:ref:`установки <setup-tools-ru>`.
Вам также понадобится модуль смарт-контракта в Wasm для моделирования.

.. todo::

   Написать остальное, когда все будет готово.

Моделирование создания экземпляра
=================================

Чтобы смоделировать создание экземпляра смарт-контракта с помощью
``cargo-concordium``, выполните следующую команду:

.. code-block:: console

   $cargo concordium run init --module contract.wasm \
                               --contract "my_contract" \
                               --context init-context.json \
                               --amount 123456.789 \
                               --parameter-bin parameter.bin \
                               --out-bin state.bin

``init-context.json`` (используется с параметром `--context``) - это файл,
содержащий контекстную информацию, такую как текущее состояние сети,
отправитель транзакции и учетная запись, вызвавшая эту функцию.
Примером такого контекста может быть:

.. code-block:: json

   {
       "metadata": {
           "slotTime": "2021-01-01T00:00:01Z"
       },
       "initOrigin": "3uxeCZwa3SxbksPWHwXWxCsaPucZdzNaXsRbkztqUUYRo1MnvF",
       "senderPolicies": [{
           "identityProvider": 1,
           "createdAt": "202012",
           "validTo": "202109"
       }],
   }

.. seealso::

   Для справки о контексте см. :ref:`simulate-context`.


Моделирование обновлений
========================

Чтобы смоделировать обновление экземпляра смарт-контракта с помощью
``cargo-concordium``, выполните:

.. code-block:: console

   $cargo concordium run update --module contract.wasm \
                                 --contract "my_contract" \
                                 --func "some_receive" \
                                 --context receive-context.json \
                                 --amount 123456.789 \
                                 --parameter-bin parameter.bin \
                                 --state-bin state-in.bin \
                                 --out-bin state-out.bin

``receive-context.json`` (используется с параметром ``--context``) - это файл,
содержащий контекстную информацию, такую как текущее состояние сети,
отправитель транзакции, учетная запись, вызвавшая эту функцию, и
учетная запись или адрес, отправившие текущее сообщение.
Примером такого контекста может быть:

.. code-block:: json

   {
       "metadata": {
           "slotTime": "2021-01-01T00:00:01Z"
       },
       "invoker": "3uxeCZwa3SxbksPWHwXWxCsaPucZdzNaXsRbkztqUUYRo1MnvF",
       "selfAddress": {"index": 0, "subindex": 0},
       "selfBalance": "0",
       "sender": {
           "type": "account",
           "address": "3uxeCZwa3SxbksPWHwXWxCsaPucZdzNaXsRbkztqUUYRo1MnvF"
       },
       "senderPolicies": [{
           "identityProvider": 1,
           "createdAt": "202012",
           "validTo": "202109"
       }],
       "owner": "3uxeCZwa3SxbksPWHwXWxCsaPucZdzNaXsRbkztqUUYRo1MnvF"
   }

.. seealso::

   Для справки о контексте см. :ref:`simulate-context`.
