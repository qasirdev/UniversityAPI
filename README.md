# University-Web API with EF 6.1.3
You can build Web API in VS2013 and EF 6.1.3 code first from existing database

## Easy steps to setup Web API with EF code first in VS 2013  
#### [Step by Step guide click here for word document to download](https://github.com/qasirdev/UniversityAPI/blob/master/Pictures/Step%20by%20Setp.docx) 

- Restore data base in SQL Server 2014 [Click here](https://github.com/qasirdev/UniversityAPI/tree/master/Database) 

#### ![image](https://github.com/qasirdev/UniversityAPI/blob/master/Pictures/Database-diagram-small.jpg)

#### Steps for New Project in VS 2013 
	- Create New Web project 
	- Select Web API with MVC and no authentication 
    - Install EF 6.1.3 for Code first from existing database 
    - Create a new folder DAL, and right click select Add New Item 
        - Select Data option with ADO.NET Entity Data Model 
        - Select Code first from Database 
        - Create new connection with SQL server, and select School database 
        - Select tables which you want to include in model 
		
#### Create an API folder where you will put API controllers 
	- Right click on API folder to add Controller 
	- In controller, select Web API 2 Controller with actions, using Entity Framework 
	- For Course table create controller.  
	- If receive an error then try to rebuild project before adding controller. 

#### Now Web API project is ready to test 
	- Before run, for re-reference looping add following line at App_Start/WebApiConfig/Register 
         config.Formatters.JsonFormatter.SerializerSettings.ReferenceLoopHandling = Newtonsoft.Json.ReferenceLoopHandling.Ignore; 
	- For JSON results add following Configure function at App_Start/WebApiConfig/Register   
         
        public static void Configure(HttpConfiguration config)
        {
            var json = config.Formatters.JsonFormatter;
            json.SerializerSettings.PreserveReferencesHandling = Newtonsoft.Json.PreserveReferencesHandling.Objects;
            config.Formatters.Remove(config.Formatters.XmlFormatter);

        }
	- For Lazy Loading use following code at DAL/SchoolModel.cs/constructor 
         this.Configuration.LazyLoadingEnabled = false; 

#### Run project and you will be able to see running Web API like 
	http://localhost:64238/  

#### In chrome extension "Postman" you can see JSON results by browsing URL : 
	http://localhost:64238/api/Courses 
#### If you like to add department with this JSON results, the use following code in Course API controller
	return db.Courses.Include(d => d.Department);


