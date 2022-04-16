# Validation Rules

Validation rules verify that the data a user enters in a record meets the CirclePay standards.

Parmeter| Type | Validation Rule | Error&nbsp;Message
--------- | ----------|------------|--------
Email   | Text | Max length(chr) - 50 characters<br> Min length(chr) - NA<br> Must be a valid email format | "The email must be less than 50 characters"<br>"The provided email isn't valid"<br>"The email is required"