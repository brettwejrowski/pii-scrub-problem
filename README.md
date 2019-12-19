Scrub Personal Identifying Information Problem
==================================================

Application event tracking to external services often involves meta data about the user who took the action. When this event information is sent to a third party, we want to scrub all personally identifying data reported, without losing information about what fields were actually recorded.

In order to do this on different platforms, it is useful to implement a method called `scrub()` that will take a JSON object and an array of senstive fields as an input and returns a modified JSON object that replaces alphanumeric characters with an asterisk ("\*") from values corresponding to keys matching the senstive field names.

For example, if the senstitive fields we want to "scrub" are `name`, `phone`, and `email`, a JSON input of:

```
{
  "name": "Kelly Doe",
  "email": "kdoe@example.com",
  "id": 12324,
  "phone": "5551234567"
}
```

should return:

```
{
  "name": "***** ***",
  "email": "****@*******.***",
  "id": 12324,
  "phone": "**********"
}

```


## Requirements

You will need to implement a command line executable that takes two arguments: a text file with a list of senstive fields and a JSON file of user data to scrub. Calling `./scrub sensitive_fields.txt input.json ` should output a scrubbed JSON version of `input.json` with the keys in `senstive_fields.txt` "scrubbed".

Any valid JSON input should be able to be handled. Value types for senstive keys should be handled as follows:
  - `String`: replace alphanumeric characters with "*"
  - `Number`: convert to string and replace alphanumeric characters with "*"
  - `Boolean`: replace entire value with "-"
  - `Array`: each value of the array should be evaluated as described by other field types
  - `Object`: if the key matches a senstive field, all values of the nested object should be scrubbed as described by other field types. If the nested object does not correspond to a senstive key, each key/value pair of the nested object should be evaluated as described by other field types
  - `null`: value should be unmodified


## Tests

A handful of example test "scrubs" are in the `/tests/` directory. Each subdirectory has an `input.json`, `sensitive_fields.txt`, and corresponding `output.json` that is expected.

**You should spend no more than 1.5 hours on this problem, and prioritize the test examples by prefixed number**. You are not expected to have completed all tests; simply work through accomodating them incrementally in the time allotted.
