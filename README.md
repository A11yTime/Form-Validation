## Accessibility Consideration of Form Validation
* Focus must be send to the error related field when error occur
* Error message must be programmatically determined with the associated field
  
### Terminology
* aria-describedby="id" Programmatically determined error message with associated field
* ref="id" Define the target of sending focus
* v-model: Two ways binding of forms and data
* indicates the entered value does not conform to the format expected by the application/ Input is Invalid
* role="alert": Make announcement for screen reader of success message.
