.. highlight:: toml

.. _setup-contract-ru:

=================================
Настройка проекта смарт-контракта
=================================

Смарт-контракт в Rust написан как обычная библиотека Rust.
Затем библиотека компилируется в Wasm с использованием целевого объекта Rust
``wasm32-unknown-unknown`` и, поскольку это всего лишь библиотека Rust,
мы можем использовать Cargo_ для управления зависимостями.

Чтобы настроить новый проект смарт-контракта, сначала создайте каталог проекта.
Внутри каталога проекта выполните в терминале следующее:

.. code-block:: console

   $cargo init --lib

Это позволит настроить проект библиотеки Rust по умолчанию, создав несколько
файлов и каталогов.
Теперь ваш каталог должен содержать файл ``Cargo.toml`` и ``src``
каталог и некоторые скрытые файлы.

Чтобы иметь возможность сборки Wasm, нам нужно сообщить cargo правильный ``crate-type``.
Это делается путем добавления следующего содержимого в файл ``Cargo.toml``::

   [lib]
   crate-type = ["cdylib", "rlib"]

Добавление стандартной библиотеки смарт-контрактов
==================================================

Следующий шаг - это добавить ``concordium-std`` в качестве зависимости.
Это библиотека для Rust содержит процедурные макросы и функции
для написания небольших и эффективных смарт-контрактов.

Библиотека добавляется путем открытия ``Cargo.toml`` и добавления строки
``concordium-std = "*"`` (желательно заменить `*` на последнюю версию `concordium-std`_) в
разделе ``[dependencies]``::

   [dependencies]
   concordium-std = "0.4"

Документацию можно найти на docs.rs_.

.. note::

   Если вы хотите использовать модифицированную версию, вам придется клонировать
   репозиторий с помощью ``concordium-std`` и вместо этого иметь точку зависимости
   в каталоге, добавив следующее в ``Cargo.toml``::

      [dependencies]
      concordium-std = { path = "./path/to/concordium-std" }

.. _Rust: https://www.rust-lang.org/
.. _Cargo: https://doc.rust-lang.org/cargo/
.. _rustup: https://rustup.rs/
.. _repository: https://gitlab.com/Concordium/concordium-std
.. _docs.rs: https://docs.rs/crate/concordium-std/
.. _`concordium-std`: https://docs.rs/crate/concordium-std/

Готово! Теперь вы можете разработать свой собственный смарт-контракт.
