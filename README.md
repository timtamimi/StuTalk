<header>

## SITS-out integration via Stu Talk 1.0

In this step-by-step guide, we are going to go through the process of setting up an export data feed out of SITS and into a web-based product, using Stu Talk 1.0.

</header>

* * *

<div class="row">

<div class="col-md-12">

*   In this example, our recipient is [Azorus CRM](https://azorus.com/) via HTTP requests.
*   In this example, we are publishing changed records in the STU table.

The screens we are going to need in SITS are:

*   DOT
*   EOT
*   TOT
*   SMP
*   TUP
*   DOR
*   EOR
*   SMG
*   XET
*   WRF
*   FMU
*   FTY
*   FTS

* * *

### Message Group (SMG)

The first thing we need to do is to specify a name for our group of “messages” (Messages in this context refers to an exchange of data in/out of SITS).

To do this, we are going to go on the SMG screen.

This screen is pretty simple! Go ahead and create a message group… You can name it anything you like, just make sure you make note of the **Code** because we will need this in the following steps.

**  
Here’s what my example looks like:**

![](http://ttamimi.co.uk/read/img/1.png)

* * *

### Telling SITS which tables are subject to integration (TUP)

We are now going to go to the TUP screen. TUP stands for Table Update Process. This enables you to trigger actions based on updates that take place in a table that you specify. It looks something like this:

![](http://ttamimi.co.uk/read/img/2.png)

In this example, we want SITS to create a DOT record for each change. We will come back to DOT records a little later.

Here's a brief explanation of each field on this screen:

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

Field name

</td>

<td colspan="1" rowspan="1">

What does it do?

</td>

<td colspan="1" rowspan="1">

Example

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Dictionary code

</td>

<td colspan="1" rowspan="1">

Specifies which Uniface Dictionary (DCT) contains the entities/fields that we want to monitor.

</td>

<td colspan="1" rowspan="1">

“MENSYS”, “SRS” or “CAMS”...

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Entity code

</td>

<td colspan="1" rowspan="1">

Specifies which table in particular you are monitoring within the dictionary.

</td>

<td colspan="1" rowspan="1">

“STU”, “DPT” or “CAP”...

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Table Update Group

</td>

<td colspan="1" rowspan="1">

A unique code that identifies this particular TUP entry.

</td>

<td colspan="1" rowspan="1">

In this example, we are going to use “AZR_STU”.

The “AZR” is because it’s for integrating with a CRM called ‘Azorus’ and the “STU” is because we’re looking at the STU table.

You can enter anything you like - as long as it’s unique and it should ideally be something that makes sense to other users of the system (human-readable).

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Rank

</td>

<td colspan="1" rowspan="1">

Tells SITS the position of this TUP in the queue of TUPs. This is important if you have multiple TUPs looking at the same entity.

It’s a required field, maximum of four digits.

</td>

<td colspan="1" rowspan="1">

1, 2, 3…

100, 9999...

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Active

</td>

<td colspan="1" rowspan="1">

Self explanatory - if this is not ticked, the TUP will not do what it’s supposed to do!

This can be useful for troubleshooting.

</td>

<td colspan="1" rowspan="1">

Boolean.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Bath/Group

</td>

<td colspan="1" rowspan="1">

This field is a way by which you can group your TUPs.

</td>

<td colspan="1" rowspan="1">

In our example, we used “AZORUS” as the group name, and we gave this group name to all TUPs that are there for the purpose of integrating SITS with our instance of Azorus.

You can name the group anything you like. You are advised to keep it simple and human-readable.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Trace Mode

</td>

<td colspan="1" rowspan="1">

If this is ticked, you will be able to see more information in the Message Buffer when something changes.

This can be useful for troubleshooting.

</td>

<td colspan="1" rowspan="1">

Boolean.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Updated by

and

Owned by

</td>

<td colspan="1" rowspan="1">

A PRS code specifying which user is responsible for the TUP, and who has updated it.

This is useful for governance purposes (having an audit trail of sorts).

</td>

<td colspan="1" rowspan="1">

The value will depend on your PRS code structure. In this example, my username is “TAMT1”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Description

</td>

<td colspan="1" rowspan="1">

A description of what the TUP is meant to do…

It sounds silly, but as you have more and more TUPs build up, this will be very useful.

</td>

<td colspan="1" rowspan="1">

Anything that’s 255 characters or fewer.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Update type

</td>

<td colspan="1" rowspan="1">

This the most important bit! It tells the TUP what to do exactly in the event of an update in the table.

</td>

<td colspan="1" rowspan="1">

As we are using Stu Talk 1.0, you have two options…

*   Stu-Talk: Data change (DOT)
*   Stu-Talk: Transfer-out-Tray (TOT)

The “TOT” is where data goes to get transferred out of SITS. If you send the changes to the “DOT” first, this enables you to manipulate the data/changes before they go to the TOT.

In our example, we are going to use the “DOT” option.

The full array of options includes:

*   Field update
*   Multi Field update
*   Build SRL style text
*   Table Update (TTU)
*   Automated Business procedure (ABP)
*   Report Query (RQH / RQI)
*   SQL command
*   Generate Standard Letter
*   Generate and Print Standard Letter
*   Stu-Talk: Data change (DOT)
*   Stu-Talk: Transfer-out-Tray (TOT)
*   Stu-Talk 2.0: Data Event

![](http://ttamimi.co.uk/read/img/3.png)

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Expiry Type

</td>

<td colspan="1" rowspan="1">

Enables you to specify an Expiry Type.

Expiry Types are defined in the XPT screen.

</td>

<td colspan="1" rowspan="1">

In our example, we want the TUP to run indefinitely, so we will leave this field blank.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Message Group

</td>

<td colspan="1" rowspan="1">

Enables you to specify which Message Group (SMG) this TUP belongs to...

</td>

<td colspan="1" rowspan="1">

In the previous step, we created a Message Group called “AZORUS”, so we will enter this Code here.

You should enter whichever Code you specified when creating your Message Group in the SMG screen.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Message Line Text

</td>

<td colspan="1" rowspan="1">

A brief message that comes up in the Message Buffer when a DOT record has been created.

We will come back to DOT records later on, but it’s essential a way for SITS to let you know that the TUP is working. This is useful for troubleshooting purposes.

</td>

<td colspan="1" rowspan="1">

This can be anything you like. In our case, we have a message that says “DOT created”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Create audit

</td>

<td colspan="1" rowspan="1">

The field contorls whether or not this TUP generates a TAR record (TUP Audit Report).

</td>

<td colspan="1" rowspan="1">

Options are:

1.  No Audit report
2.  Audit if conditions met
3.  Always create audit

Options 2 and 3 are useful for testing. Option 1 is more suitable for a Live environment (post-testing) since creating the Audit records can be demanding in terms of server performance.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Process for New record

</td>

<td colspan="1" rowspan="3">

This is where you specify when you want your TUP to trigger a change record (thereby creating a DOT record).

In our example, we specified that we want records to be processed “before store” for new records and when records are updated, but not when records are deleted.

In the example of a CRM integration with the STU table, this means that if a new record is created in SITS, a mirroring record will appear in the CRM. If a record is updated in SITS, the same data will appear in the CRM. However if a STU record is deleted in SITS, the counterpart in the CRM would remain.

</td>

<td colspan="1" rowspan="3">

Boolean - either “No Action” or “Before”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Process for Update

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Process for Delete

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

First condition

</td>

<td colspan="1" rowspan="2">

You can create conditions to specify under which circumstances you want the TUP to kick-in. We are going to leave those blank for this example because we will specify our conditions (or “Rules”) at the Data Tray level in the following steps.

</td>

<td colspan="1" rowspan="2">

We left those blank, however you can click on the Edit icon if you wish to add conditions.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Second condition

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Client or Web

</td>

<td colspan="1" rowspan="1">

Specifies whether the TUP should get triggered if the change happens in the Client and/or Web.

</td>

<td colspan="1" rowspan="1">

We chose “Both Client and Web” - you should select whichever option that’s fit for purpose for your particular scenario.

</td>

</tr>

</tbody>

</table>

The end result might look something like this:

![](http://ttamimi.co.uk/read/img/4.png)

* * *

### Creating DORs (DataChange-Out-Tray Rules)

The TUP we created earlier tells SITS that we want it to create “DOT” records when a change occurs. That’s fine in theory, however with big tables like STU, you wouldn’t always want every change to be recorded. This is where DORs come in.

DOR allows you to specify the exact circumstances under which a DOT record should be created.

The screen looks something like this:

![](http://ttamimi.co.uk/read/img/5.png)

We’re going to start by specifying a “DOR Code” - We recommend that you use a code that is somewhat consistent with what you have called the respective TUP process you created earlier. In our case, we are going to call this DOR “AZORUS_STU”.

You can then give it a Short Name, a Full Name, and a Description of your choosing.

Make sure that you select your Stu Talk Version. We are using Stu-Talk 1.0.

Also make sure that you have activated the DOR by ticking the box next to “Active Rule”.

For “Batch” and “Message Group”, we are going to use the same name that you have specified in your SMG screen earlier. In our example this will be “AZORUS”.

We are then going to specify “Link Dictionary” and “Link Entity” just as we did when creating the TUP. In our example this is “SRS” and “STU” respectively.

The “Link Value” is essentially your Primary Key. This will be different depending on what table you are looking to exchange.

The format of the string should be:

_DictionaryCode.Entity~<<Field.Entity.DictionaryCode>>_

Depending on your version of SITS, you should be able to ‘automate’ this by clicking on the ‘Default’ button shown below.

![](http://ttamimi.co.uk/read/img/6.png)

That’s the hard part over. We now want to specify the circumstances under which we want a DOT record created.

In our example, we only want a DOT record to be created if those particular fields are altered:

*   Applicant status code (STU_STA1)
*   Student status code (STU_STA2)
*   Student Title (STU_TITL)
*   First name 1 (STU_FNM1)
*   Surname (STU_SURN)
*   Student date of birth (STU_DOB)
*   Gender (STU_GEND)
*   UK Residency (STU_RSDT)
*   Undefined Data Field B (STU_UDFB)

We’re going to create those one by one…

Start by clicking the “Add” button.

![](http://ttamimi.co.uk/read/img/7.png)

This will create a row. You can now start by populating the “Old field / Value” column in the following format:

_“<<Field.Entity>>”_

You can then set the operator. In this scenario, we are comparing the existing value with the new value, and we are telling SITS that if those values are in any way different, log a DOT record, so our operator is going to be != but you should select whichever operator that is applicable to your integration.

You can now drop the same field name in the “New field / Value” column.

You should now have something like this:

![](http://ttamimi.co.uk/read/img/8.png)

You can now repeat the process for adding more fields. Just make sure you join your various rules with an operand. In our case, we are going to use the Operand != because we want to detect any change in any of the fields listed.

Adding a second field to compare should give us this:

![](http://ttamimi.co.uk/read/img/9.png)

We repeat this for each field we want to monitor…

The end result might look something like this:

![](http://ttamimi.co.uk/read/img/10.png)

That’s your DOR done.

So what we have achieved so far is a rule whereby if any of the fields listed above change on a STU record, a corresponding “DOT” record will be created to represent this change. Go ahead and try it.

Example:

I went to the STU screen and created a new record with the following information:

![](http://ttamimi.co.uk/read/img/11.png)

I noticed that my message buffer shows the following:

![](http://ttamimi.co.uk/read/img/12.png)

And this tells me that my TUP is working!

Now if I go on the DOT screen and I retrieve the most recent record, I get this:

![](http://ttamimi.co.uk/read/img/13.png)

DOR is all done.

* * *

### Creating the XET (part 1 of 2)

XET is the “Exchange Template” screen. We are going to come back to this screen a little later to parse our data so that the recepient system knows how to read it, but for now we just need to create the XET record…

Go ahead and fire up the XET screen. It looks something like this:

![](http://ttamimi.co.uk/read/img/14.png)

We need to specify the following fields:

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

Field

</td>

<td colspan="1" rowspan="1">

What to do with it

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

XET Code

</td>

<td colspan="1" rowspan="1">

Give it a unique code.

I suggest being consistent and using the same unique reference that you used for creating the DOR/TUP. So in my example, I am going to give my XET code “AZORUS_STU”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Short Name

Full Name

Description

</td>

<td colspan="1" rowspan="1">

This can be anything you like. It’s recommended that you keep this simple and human-readable.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Batch

</td>

<td colspan="1" rowspan="1">

In my example, I named the batch “AZORUS” after the SMG that we created earlier on.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Dictionary

</td>

<td colspan="1" rowspan="1">

In our example this is “SRS”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Entity

</td>

<td colspan="1" rowspan="1">

In our example this is “STU”.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

In use

</td>

<td colspan="1" rowspan="1">

Make sure this is switched on, otherwise the XET is not in effect.

</td>

</tr>

<tr>

<td colspan="1" rowspan="1">

Valid for Import

Valid for Export

</td>

<td colspan="1" rowspan="1">

Specify the type of exchange for which this XET would apply.

In our case, we don’t want data written back from the CRM into SITS, so we only ticked “Valid for Export”.

</td>

</tr>

</tbody>

</table>

You can leave the rest for now… And your XET should look something like this:

![](http://ttamimi.co.uk/read/img/15.png)

We will come back to XETs later.

* * *

### Creating your EOR (DataEvent-out-tray Rule)

Let’s take a step back… Before creating the XET, we created a DOR which told SITS under which circumstances do we want it to create a DOT record.

DOT records are sort of like audit trails. In order to actually utilise them in a data exchange, we need to process them into “EOT” records.

In the same way that DOTs get created based on a DOR, EOTs are created according to an EOR.

Go ahead and fire up the EOR screen. It looks like this:

![](http://ttamimi.co.uk/read/img/16.png)

Here’s what we want to do on this screen:

1.  Give it a code. We are going to be consistent and use the same code as we did when creating the DOR and the XET, so we are using “AZORUS_STU”.
2.  Give it an appropriate short name, full name, and description.
3.  Mark the EOR as “Active” by ticking the box.
4.  Give the EOR a “Rank” which tells SITS in which order to process it relative to other EORs.
5.  Change the “Version” to “Stu-Talk 1.0” - this will change what fields are available under the “Message Details” section.
6.  Specify the Dictionary in the “Link Dictionary” field. Ours is “SRS”.
7.  Specify the “Link Entity” which in this example is “STU”.
8.  Specify the “Message group” according to your SMG. Ours is “AZORUS”.
9.  Change the “Mark as Processed” to “All EOTs Including Open”.
10.  Set “XET” code to the XET code that you created in the previous step. Ours will be “AZORUS_STU”.

_Explanation: What this does is it 'ticks' EOT records that have already been processed as Processed so that they don't get re-processed which can clog up your message queue._  

Next, we are going to start configuring the “Message Details” section. Please note that the configurations here will vary depending on where you are trying to push your message. In this example, we are pushing data from SITS into a Cloud-based CRM in the form of HTTP requests. Here is what we did:

1.  Specify the message type as “HTTP”
2.  Click on the button next to ‘Parameter’

![](http://ttamimi.co.uk/read/img/17.png)

1.  A sub-screen (shown below) will pop up.

![](http://ttamimi.co.uk/read/img/18.png)

You should configure this screen according to your receiving end’s requirements. In our case, we are sending HTTP POST requests, so I have set the URL post mode to “POST”, the URL destination is where the requests are being send to, the Username and Password are defined according to the receving end (assuming authentication is required). You may also want to set HTTP Headers. Lastly, make sure you define your HTTP Success codes! This is what tells SITS whether the transfer has been successful or not. Normally, success codes are three digits and start with a 2\. E.g. 200, 201, 202… etc

You can find a list of generic HTTP codes here: [https://httpstatuses.com/](https://www.google.com/url?q=https://httpstatuses.com/&sa=D&ust=1482230805742000&usg=AFQjCNHCa6W17v8WgETb2wdVx5FdFvkurg)

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

TIP: When I was setting this up, it didn’t work and I couldn’t work out what the issue was… After some digging around, I found that the “Password” field in SITS translates into the following header:

PSWD=xxxxxxxxxxxx

Whereas our CRM was expecting the authentication to come via the following header:

PASSWORD=xxxxxxxxxxxx

You can work around this by putting the password in as plain text in the headers field, instead of putting it in the password field. The downside of this approach is that the password doesn’t get processed through the SITS MD5 hash, and therefore it is completely open to anyone with access to the EOR screen in the client, so this is not advisable.

</td>

</tr>

</tbody>

</table>

When you’re done, press Apply. You should now be all done in terms of your EOR set up. Here’s what our final EOR looks like:

![](http://ttamimi.co.uk/read/img/19.png)

* * *

### What now?

At this point, when you make a change, a DOT record is created to document it. However if this is your first time using Stu Talk, you will notice that no EOTs are being created afterwards. Don’t panic.

The EOTs are created by processing the DOTs. This happens when the Stu Talk monitor runs.

In order to get DOTs processed into EOTs, we need to run the monitor. In order to do this, you will need to log into your SITS Server, or at least be on a machine with access to the Server.

We then also need to get EOTs turned into TOTs. TOT stands for “DataTransfer-out Tray” and it’s the bit that actually send the EOTs out of SITS. Unlike the way we needed to create DORs for DOTs and EORs for EOTs, you don’t need to configure anything for TOTs to work.

Let’s get started. Go ahead and fire up your server. I’m using Remote Desktop Connection to do this.

![](http://ttamimi.co.uk/read/img/20.png)

Once your server is up, start a Command Line screen (CMD)

The commands you need to run will vary depending on your SITS set up and configuration, however they will be something along those lines:

Command 1 (Process DOT records into EOTs):

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=0 maxtime=5:00:00 DOT</span>

Command 2 (Process EOT records into TOTs):

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=0 maxtime=5:00:00 EOT</span>

Command 3 (Send TOTs out of SITS):

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=3 maxtime=5:00:00 TOT</span>

Please note that the smg_code parameter is set to whatever your SMG group is called. Our is Azorus.

Please also ensure that your usr_code parameter is set to a username for a user that has admin access in SITS Client.

FAQ: Why did you set TOT to repeat three times?

I found that the TOT processing seems to fail for various reasons so by repeating it, that seems to take care of the issue. It may be a problem that you won’t encounter.

At this stage, I found the SMP screen very helpful. SMP [in a quirky Tribal way] stands for “StuTalk Monitor Process Map”, and it allows you to check that your transfers are going through each of the stages, from DOTs, to EOTs, to TOTs.

At this stage, your mechanism should be all working. Go ahead and test it…

1.  Make a change to your data. (In the example we did previously, I created a STU record for a student called Bert Reynolds, with STU Code 90909090)
2.  Check that a DOT has been created. You can test this through multiple ways...

a. You can check in the DOT screen. It should show something like this:

![](http://ttamimi.co.uk/read/img/21.png)

b. You can check the SMP screen. It should show something like this:

![](http://ttamimi.co.uk/read/img/22.png)

c. You can check in the SMD (Stu Talk Monitor Details) screen.

1.  Run the following two commands (sequentially) in your command line (Change the exact details to match your configuration)

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=0 maxtime=5:00:00 DOT</span><span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=0 maxtime=5:00:00 EOT</span>

You can also join them together in one command if you want:

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=0 maxtime=5:00:00 DOT EOT</span>

However it’s best if you don’t combine the TOT in the same combined command as that one seems to fail more regularly and requires slightly different configuration.

1.  Check that the EOT record has been created. Again, you can do this in the EOT screen, and it would look like this:

![](http://ttamimi.co.uk/read/img/23.png)

Or you can check the SMP/SMD screens too. The SMP screen would look something like this:

![](http://ttamimi.co.uk/read/img/24.png)

1.  You can now run your TOT command...

<span style="color: #0000ff;">\\NameOfYourServer\sits_clients\vision\live\uniface\bin\uniface.exe /asn=X:\siapp\vision\live\adm\svrsipr_stutalk.asn stutalk usr_code=XXX xpt_code=APP_IN tracemess=3 smg_code=AZORUS limit=0 pause=0 repeat=3 maxtime=5:00:00 TOT</span>

1.  Check that TOT was created. The TOT record's presence confirms that SITS has fired the data out. You can check this in the TOT screen, which would look like this:

![](http://ttamimi.co.uk/read/img/25.png)

or in the SMP screen, which would look like this:

![](http://ttamimi.co.uk/read/img/26.png)

OK, so the message is sent, but the TOT record is saying that the B2B Message status returned is 406 which is not a success code.

Let's have a look at the receiving end in Azorus CRM:

<table>

<tbody>

<tr>

<td>

Response Body

Failed: Unable to import Lookup Data: Unknown or unsupported Lookup [STU]

</td>

</tr>

</tbody>

</table>

So we know that SITS has successfuly reached out to Azorus, but the message was not interpreted correctly. To fix this, we need to go back and examine our XET...

* * *

### Creating the XET (part 2 of 2)

Earlier, we created an XET with code “AZORUS_STU”. The XET seems to work in the sense that messages are being sent to our CRM, but the CRM is not able to interpret those messages.

This is a situation where we can use XSL (or XSLT) to manipulate the format of the XML message that is being sent.

On the XET screen, you will notice that there is a “XSL Options” tab. It looks something like this:

![](http://ttamimi.co.uk/read/img/27.png)

This enables us to add an XSL(T) file which would act like an adapter, translating the XML labels into the relevant strings for your recipient.

In order to utilise this, we need to:

1.  Create an XSL(T) file
2.  Upload the file to SITS
3.  Link the file to the XET

**Step 1.** Create an XSL(T) file

XSL(T) is a fairly simple syntax. The exact syntax of your XET file will vastly depend on what fields you are pulling from SITS and where you are pushing them to…

For the sake of having an example, this is what part of ours looks like:

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:ext="http://exslt.org/common" version="1.0">

<xsl:output indent="yes" method="xml"/>

<xsl:template match="/">

<xsl:variable name="FullDocument">

<EXCHANGE>

<person>

<xsl:for-each select="EXCHANGE/STU/STU.SRS" >

<!-- Ids -->

<sitsId>

<xsl:value-of select="MRE/MRE.MENSYS/MST/MST.SRS/MST_CODE.MST.SRS" />

</sitsId>

<azorusId>

<xsl:value-of select="MRE/MRE.MENSYS/MST/MST.SRS/MST_UDF1.MST.SRS" />

</azorusId>

<studentCode>

<xsl:value-of select="STU_CODE.STU.SRS" />

</studentCode>

<uniqueLearnerId>

<xsl:value-of select="STU_UNLN.STU.SRS" />

</uniqueLearnerId>

</xsl:for-each>

</person>

</EXCHANGE>

</xsl:variable>

</xsl:template>

<xsl:template match="@* | node()">

<xsl:copy>

<xsl:apply-templates select="@* | node()"/>

</xsl:copy>

</xsl:template>

<xsl:template match= "*[not(@*|*|comment()|processing-instruction()) and normalize-space()='']"/>

</xsl:stylesheet>

</td>

</tr>

</tbody>

</table>

Let’s drill down into one particular field…

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

<sitsId>

<xsl:value-of select="MRE/MRE.MENSYS/MST/MST.SRS/MST_CODE.MST.SRS" />

</sitsId>

</td>

</tr>

</tbody>

</table>

Line 1 contains the tag <sitsID> which is the way that Azorus expects this piece of information to be labelled.

Line 2 pulls the value of the field MST_CODE in the MST table in the SRS entity.

Line 3 closes the tag <sitsID>

You can use this format to create additional conversions, for example, the lines below transcribe the country of domicile code which is normally labelled STU_CODC in the STU table in SITS, into a field called ‘countryOfDomicileCode’:

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

<countryOfDomicileCode>

<xsl:value-of select="STU_CODC.STU.SRS" />

</countryOfDomicileCode>

</td>

</tr>

</tbody>

</table>

...and here’s another example in which we transcribe the Gender field to “genderCode”:

<table>

<tbody>

<tr>

<td colspan="1" rowspan="1">

<genderCode>

<xsl:value-of select="STU_GEND.STU.SRS" />

</genderCode>

</td>

</tr>

</tbody>

</table>

**Step 2**. Upload the file to SITS.

In order to do this, we are going to use four screens. They are:

1.  FTY
2.  FTS
3.  FMU
4.  WRF

1.  Start with FTY: FTY screen enables you to define that a set of files has a certain file type, and that those files are getting dumped in a particular location in one of your SITS Servers.

The screen looks like this:

![](http://ttamimi.co.uk/read/img/28.png)

Note that the menu of options under “Client or Server” does contain an option called XSL Transformation Server which is where you would ideally put these files and have them processed, reducing the processing load off your Client server, however in this particular example, an XSL Transformation Server is not available to us, so we are putting the files on the Client Server. This generally should not matter as long as your server can handle the load, and as long as you have read/write permission on the destination.

1.  We can now move to the FTS screen. Create a record that looks like this:

![](http://ttamimi.co.uk/read/img/29.png)

The settings in FTS will mirror your options in FTY.

1.  With FTS and FTY set up, you should now go to FMU to upload the file(s). The FMU screen looks like this:

![](http://ttamimi.co.uk/read/img/30.png)

What you do here depends on where you are uploading the files from.

I'm uploading my XSLT from my local machine, so I selected a directory where it says Export / Import Directory and I then clicked on the button for option 4.

1.  And finally, once FTS and FTY are set up, and you have uploaded your files via FMU, you can now go to WRF to Publish the file(s) you uploaded!

The WRF screen looks something like this:

![](http://ttamimi.co.uk/read/img/31.png)

The reason we need to go to the WRF screen is because while the FMU screen uploads the files to the server, WRF manages the publishing process which makes those files usable.

**Step 3.** With our XSLT uploaded and published, we’re now going back to the XSL Options tab in the XET screen, and then go ahead and click on the Edit button shown below:

![](http://ttamimi.co.uk/read/img/32.png)

You will see a pop up screen which looks something like this:

![](http://ttamimi.co.uk/read/img/33.png)

You’ll notice that the XET code is pre-populated for you.

Under “Record Type”, we are going to select “Export” because the information is flowing out of SITS only.

Under “Mode” we are going to select ‘Transform’.

We are then going to enter our WRF code, as taken from the previous step.

Make sure you tick the ‘Active’ box, otherwise the XST will not apply and the data labels will not get transformed.

Your final screen should look like this:

![](http://ttamimi.co.uk/read/img/34.png)

And you’re all set.

You can now make a change in the STU table. This should create a DOT.

Once the store is completed, you can then run your monitors as shown earlier, which will create your EOT and TOT records, and fire off the HTTP request to your recipient.
