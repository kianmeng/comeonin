# Comeonin [![Build Status](https://travis-ci.org/riverrun/comeonin.svg?branch=master)](https://travis-ci.org/riverrun/comeonin) [![Hex.pm Version](http://img.shields.io/hexpm/v/comeonin.svg)](https://hex.pm/packages/comeonin)

Password hashing (bcrypt, pbkdf2_sha512 and one-time passwords) library for Elixir.

This library is intended to make it very straightforward for developers
to check users' passwords in as secure a manner as possible.

Comeonin supports `bcrypt` and `pbkdf2_sha512`.

## Features

* Comeonin uses the most secure, well-tested, and up-to-date hashing schemes.
* It uses the latest version of bcrypt, supporting the $2b$ prefix.
* It is easy to use.
    * Salts are generated by default.
    * Each function has sensible, secure defaults.
* It provides excellent documentation.
    * Clear instructions are given on how to use Comeonin.
    * Several recommendations are also given to help developers keep their apps secure.

### Argon2 support

At the moment, Comeonin does not support Argon2, the winner of the 2015
Password Hashing Competition, and there are no plans to support it in
the near future. See [this issue](https://github.com/riverrun/comeonin/issues/65)
for more details.

## Requirements and build errors

See the [Requirements](https://github.com/riverrun/comeonin/wiki/Requirements)
page in the wiki for details.

## Installation

1. Add comeonin to your `mix.exs` dependencies

  ```elixir
  defp deps do
    [ {:comeonin, "~> 2.6"} ]
  end
  ```

2. List `:comeonin` as an application dependency

  ```elixir
  def application do
    [applications: [:logger, :comeonin]]
  end
  ```

3. Run `mix do deps.get, compile`

4. Optional: during tests (and tests only), you may want to reduce the number of bcrypt,
or pbkdf2, rounds so it does not slow down your test suite. If you have a `config/test.exs`,
you should add (depending on which algorithm you are using):

  ```elixir
  config :comeonin, :bcrypt_log_rounds, 4
  config :comeonin, :pbkdf2_rounds, 1
  ```

  NB: do not use the above values in production.

## Usage

Either import or alias the algorithm you want to use -- either `Comeonin.Bcrypt`
or `Comeonin.Pbkdf2`.

Both algorithms have the `hashpwsalt` function, which is a convenience
function that automatically generates a salt and then hashes the password.

To hash a password with the default options:

    hash = hashpwsalt("difficult2guess")

See each module's documentation for more information about
all the available options.

To check a password against the stored hash, use the `checkpw`
function. This takes two arguments: the plaintext password and
the stored hash:

    checkpw(password, stored_hash)

There is also a `dummy_checkpw` function, which takes no arguments
and is to be used when the username cannot be found. It performs a hash,
but then returns false. This can be used to make user enumeration more
difficult.

## Documentation

http://hexdocs.pm/comeonin

## License

BSD. For full details, please read the LICENSE file.
