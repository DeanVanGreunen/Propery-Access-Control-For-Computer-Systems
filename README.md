# Propery Access Control For Computer Systems.

### Description:
>	This White Paper Describes how to properly setup safe and secure ACLs wihin the Backendt of any computer system.
>	This is written for other existing and new system designs with minor configurations for your unique system setup/design.

##### Publisher
**Author**: [Dean Van Greunen](https://github.com/DeanVanGreunen)

**Publisher**: [Dean Van Greunen](https://github.com/DeanVanGreunen)

**License**: [FREE](https://en.wikipedia.org/wiki/Intellectual_freedom) provided [As is](https://en.wikipedia.org/wiki/As_is)

#### Table Of Contents:
	1. Terms | Page 1
		Note: Used In Later Parts of the doc.
	
	2. Overview | Page 2
		2.1. Introduction.
		2.2. OSI Layer.

	3. Access Types | Page 3
		3.1. Users. (Either Via GUID or as Anoynmous User)
		3.2. Roles. (A Users Parent Group, A User May Have An Anoynmous user Group)
		3.3. Associated Devices and Associated Accounts.

	4. Layers | Page 4
		4.1. Network Access.
		4.2. API Call.
		4.3. Services.
		4.4. Database.
		4.5. File System.

	5. Storing ACLs For UAR and RAR  | Page 4
		5.1. Long-Term Retainable Storage.
		5.2. Memory Storage.

	6. Implementation  | Page 5
		6.1. Database/File Storage.
		6.2. Best Single Secuirty Pratice.

	7. Special Thanks | Page 6

## Page 1
	1. Terms:
	    ACLs (Access Control Layers)
		GUID (Global Unique Identifer)
		UGUID (A User's Global Unique Identifer)
		RGUID (A Roles's Global Unique Identifer)
		UAR (User Access Rights)
		UAD (User Access Data)
		RAR (Role Access Rights)
		RAD (Role Access Data)
		IP (Internet Protocal) refered normally as an IP Address.
		MAC (Media Access Control) refered normally as a MAC Address.
		OSI (Open Systems Interconnection) refered normally as the Open Systems Interconnection model.
		OS (Operating System)

## Page 2

	2. Overview:

		2.1. Introduction:

			Each Layer has its't own setup and we will not discuss the exact setup for each layers own subsystems setup or confiuration as there are many different variations.
			However we will be discussing the general and pratical usage and setup in an ideal and simple enviroment from the base or beginning system design.
			No Prerequirements are needed.

			Various Systems For the OSI Stack Existing, knowing the OSI stack would be advantageous.

		2.2. OSI Layer:
			The OSI is a 7 tiered intergrated stack usually taught in the networking class but is applicable in all fields of Development and System design.

				Layer 7: Application Layer

					What the user interacts with; This is merely the frontend if it was to be summed up in a website as an example and backend, normally the recieving side like an API or application.

				Layer 6: Presentation Layer
				
					How The Application Layer Talks With the rest of the OSI Stack, This is the mediator.

				Layer 5: Session Layer
				
					When and Who Can Talk To Me amoungst a set of connected computer systems and also says, hey, I'm available to be spoken to.
					This is like how windows can detected other computers running windows, this makes that possible and is similiar to how traffic lights works, who can say what when and also accepts or declines the requested connection.

				Layer 4: Transport Layer
				
					This allows the session layer to speak to the device that will encode the data in the next OSI; Layer 3
					Telling the Network Layer what type of connection it wants; A long term, short term or a once off connection.
					It also breaks the data to be sent into smaller easier to manage chunks. This layer also supports some error recovery.

				Layer 3: Network Layer
				
					This layer is the Who Gets The Data amoungst the connected devices.

				Layer 2: Data Link Layer
				
					This layer provides information to the Network Layer 3, which allows it to see the devices that are connected within a range.
					This layer also encodes the data into the most basic and simple data format before pushing it over the physical layer.

				Layer 1: Physical Layer
				
					This accepts the basic data format and actually sends the data via eletricity, light or Radio Signals or alternative routes in the physical world where it is governed by its own subset of system, which we wont be diving into today. 


## Page 3

	3. Access Types | Page 3
		3.1. User

			This is the basic of any security/authentication system.
			A standard user way to identify a user accessing any system.
			Either via a Registered/Assigned Account or an Anoynmous user. (These are not roles but only base account types)

		3.2. Role (A Users Parent Group, A User May Have An Anoynmous user Group)

			This is a group which a user may belong to.
			A visitor would fall under the "Guest" Role, but can also be assigned the role of "Party Assistance" at a friendly get together.

		3.3. Associated Devices and Associated Accounts.

			This would be a device that is shared to access the system such as family computer or one in an internet café.
			Accounts that are have an origin from a shared device would qualify them to be linked within the limited range of a local WiFI Router, Shared Internet connection and possibly.
			Linked as that these accounts may be locked down in the case of an issue as it could be seen as the a complice untill an investigation is completed. 


## Page 4


	4. Layers:
		4.1. Network Access | OSI 1.

			Users can be restricted by an IP and a MAC Address, however this won't block them completely but will slow them down. Forcing their system to issue them new valid IP and/or MAC Addresses.
			This should be done via the Network Systems Setup and also can be intergrated into your existing or startup web application, commanly used by firewalls but are sometimes filtered out before it reaches the firewalls.
			Note: The OS, Router, Switch and Data Exchange Gateways can all have their own seperate firewalls.

		4.2. API Call.      | OSI 7.

			User and Role can be assigned/removed a UAR and a RAR respectively using the UAD and RAD respectively in the said Database or Services Layer.

		4.3. Services.     | OSI 7 - Internal Usage.

			Allow or Deny User and/or Role Access to functions via the UAR and RAR as in 4.2

		4.4. Database.     | OSI 7 - Internal Usage Via a FileBase Database, or Another Application (May Use The Entire OSI Stack to connect to the Database System)

			Allow or Deny User and/or Role Access to Data via the UAR and RAR as in 4.2

		4.5. File System.  | OSI 7 - Internal Usage - Provided By The OS.

			Allow or Deny User and/or Role Access to Data via the UAR and RAR as in 4.2

	5. Storing ACLs For UAR and RAR:

		5.1. Long-Term Retainable Storage.

			Such as a physical file which is based on a file storage media.	Highly Recommend.

		5.2. Memory Storage.

			This would live in memory as long as the computer is switched on or until the application is restarted.

				Highly Unrecommend; Unless used for Single One Time System/Application Show Case Demo/Prototype where a full setup is required.

## Page 5

	6. Implementation
		6.1. Database/File Storage.

			Withing your structured data system such as a database like MSSQL, MySQL, NoSQL or equivalent. 

			6.1.1 Create A table per data base which will contain user and role records (one table for a role and one for a user)
				Which will store what api calls, functions, and files that they can access. see 6.2

			6.1.2 Create 2 columns on all tables which are null defaults for a both ACL Access Types:
				Which can be set to a User's GUID and Role's GUID respectively.

		6.2. Best Single Secuirty Pratice.

			Always Assume An All Deny Access Level To All Data and Functions.

				6.2.1 Mark Anonymous Functions For Public Avaiable for Un-Pre-Authed Users such as a login api call but that related account (see 3.3) can be locked out to protect incase of hacking.

				6.2.2 Ensure All Data Is Sanatized Before Entering and After Leaving the Database On route to or from the API or Service Layers.

					6.2.2.1 Only accept the data needed by your business logic, only required fields and data.

						Check The Following as well in specific order:

							- Data Size. (This will stop various memory attacks which could lead to hacks or user credentials made easier to obtain) [This will be needed to be retested after the Data Compression Test]

							- Data Compression, Don't Blindly Store, Send or Execute Compressed Data as the below checks may fail without decompressing first. then recompress after all below checks have passed; always use safe sandbox directory/memory or a disposable storage unit for this processes.

							- Data Format. (This will stop many types of attacks on the data level side)

						Test Process To Do: Size -> Compression -> Size -> Format -> Accept or Decline With Error.


## Page 6

	7. Special Thanks
		7.1. The Internet.
			To the supportive, growing and passonite inventors, developers and businesses a like; Thank you!

		7.2. All Those Have Read This White Paper.
			I hope you have learned something valuable and can may improve on this document and systems as you continually progress within your field and expertises.