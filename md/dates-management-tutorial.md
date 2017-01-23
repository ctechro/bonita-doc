# How to work with dates in process forms and BDM

Currently (until versions 7.4.x), only date selection is supported natively in the UI Designer date picker widget. So this page will only focus on date management (not date and time).

## Define your BDM data

Start by defining your Business Data model.
It is recommended that you define the date attributes of your Business Data Objects with a LONG type instead of DATE if you want the value stored in the database to reflect the date entered by the user. Otherwise the timezone of the server will be used when converting the java date in an SQL date and, unless your server is configured in UTC, an offset will be applied. This will not be an issue if you do not query the business data data base directly and only use the API as the same conversion will be performed the other way around when retrieving the value from the database. In this case, you can safely use a DATE attribute type.
Then, in the process, create a new Business variable of the type of you business object.

## Define the contract and operations/instantiation script

In the process/task contract section, use inputs of type DATE for the date attributes. The date picker widget output is an ISO 8601 formatted String ("2017-01-13T00:00:00.000Z") that will be automatically formatted to a java.util.Date by process instantiation or task execution REST API. The Date/time received will be considered as UTC. The time is set to midnight by the widget as it doesn't handle time.
The next steps depends on the way you store dates in the BDM.

### For LONG typed date attributes
If you used the LONG type instead of DATE type in the BDM for the date attributes and generate the contract using the "Add from data" feature, you need to update the contract inputs to change their types from LONG to DATE. Then in the operations or in the Business variable initialization script, you need to perform a getTime() on the DATE contract inputs in order to obtain a Long value (Milliseconds since Unix Epoch) before calling the business variable setter (which expect a Long).

### For DATE typed date attributes
If you used the DATE type in the BDM for the date attributes you can directly use the "Add from data" in the contract definition section to generate the contract and script/operations from the business variable. There is no conversion to perform.

## Generate the form from the contract

Once the contract is defined, you can generate the UI designer form by clicking on edit in the form section of the process/task execution tab.
The date picker widgets will be automatically added to the page based on the contract. There is no other operation to perform.
If you prefer to design your form manually, just keep in mind that the input expected in the contract for the dates is an ISO 8601 formatted String ("2017-01-13T00:00:00.000Z" or "2017-01-13T00:00:00Z" or "2017-01-13T00:00:00" or "2017-01-13").


