# Discover, design and run pre-built standard integrations on Edge Integration Cell

In the previous exercise we have Activated and deployed an Edge Integration Cell, let's look at how we can Discover, design and run pre-built Standard Integrations on Edge Integration Cell. In this exercise we will use a pre-built standard content to connect to S/4 HANA backend system, trigger execution of the content deployed at Edge Integration Cell and perform operations like update of the S/4 data objects.

##  Description

After completing these steps you will have created...

1. Navigate back to Home. In the Home page Navigate to Capabilities and click on "Discover Integrations" under Build Integration Scenarios tile.

![image](https://github.com/SAP-samples/teched2023-IN160/assets/12845154/58a7e175-a23a-42e0-ac95-8c3b7d32fbc2)
![image](https://github.com/SAP-samples/teched2023-IN160/assets/12845154/8c0f4666-ed16-4958-83be-e775d0e337f0)


<br>![](/exercises/ex2/images/02_01_0010.png)

3.	Insert this line of code.
```abap
response->set_text( |Hello ABAP World! | ). 
```



## Description

After completing these steps you will have...

1.	Enter this code.
```abap
DATA(lt_params) = request->get_form_fields(  ).
READ TABLE lt_params REFERENCE INTO DATA(lr_params) WITH KEY name = 'cmd'.
  IF sy-subrc = 0.
    response->set_status( i_code = 200
                     i_reason = 'Everything is fine').
    RETURN.
  ENDIF.

```

2.	Click here.
<br>![](/exercises/ex2/images/02_02_0010.png)

## Summary

You've now ...

Continue to - [Exercise 4 - Excercise 4 ](../ex4/README.md)
