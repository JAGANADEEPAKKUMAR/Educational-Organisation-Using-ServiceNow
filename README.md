Educational Organisation Using ServiceNow
1. Project Overview
The Educational Management System (EMS) is a streamlined solution built on the ServiceNow platform to enhance administrative efficiency within educational institutions. It manages student and teacher data, simplifies the admission process, and provides tools for tracking academic progress. By implementing EMS in ServiceNow, institutions benefit from a user-friendly, customizable, and automated environment that supports better decision-making and operational management.

2. Setting Up the ServiceNow Instance
Sign Up for a Developer Account
•	Visit the ServiceNow Developer Portal at https://developer.servicenow.com.
•	Create a new developer account by providing the required information.
Request a Personal Developer Instance
•	Log in to your developer account.
•	Navigate to the “Manage > Instance” section.
•	Click “Request Instance” and choose the latest available release.
•	You will receive an email with the instance details (URL, username, and password).
Access Your Instance
•	Open the instance URL received via email.
•	Log in using the provided credentials to access your personal ServiceNow instance.
 
3. Creating an Update Set
An Update Set tracks all configuration changes made in a ServiceNow instance, enabling migration between instances.
Steps:
•	Navigate to All > Local Update Sets.
•	Click New to create an update set.
•	Enter the name "Educational Organisation" and submit.
•	Click Make Current to activate the update set.
 

4. Creating the Salesforce Table
The Salesforce table manages core student information.
Steps:
•	Navigate to All > Tables > New.
•	Enter the label "Salesforce". The system will auto-generate the table name.
•	Add required fields, including:
•	Admin Number (Set Display to True, mark Extensible, and set Dynamic Default to "Get Next Padded Number").
•	Grade (Configure as a choice field with values such as Primary, Secondary, etc.).
 

5. Creating the Admission Table
This table manages data related to student admissions and extends the Salesforce table.
Steps:
•	Navigate to Tables > New.
•	Label the table as "Admission".
•	Set "Extends Table" to Salesforce.
•	Add to application menu for visibility.
•	Add necessary fields such as Admission Number, Grade, School, and Pincode.
•	Create choice fields for Admin Status, Purpose of Join, School, Pincode, and School Area.
 

6. Configuring Forms
Form configuration improves the user experience by allowing intuitive interaction with data.
Salesforce Table Form:
•	Navigate to System Definition > Tables.
•	Search for "Salesforce" and select Configure > Form Design.
•	Add and arrange relevant fields.
Admission Table Form:
•	Repeat the same process as above for the "Admission" table.
Student Progress Table Form:
•	Use the same method to configure the Student Progress table.

7. Number Maintenance for Admin Numbers
To automatically generate Admin Numbers in a specified format:
Steps:
•	Navigate to Number Maintenance > New.
•	Create a record for Admin Number.
•	Set an appropriate prefix (e.g., ADM) and define the number format (e.g., ADM0001).
•	Submit the record.
 
8. Creating Process Flows
ServiceNow Process Flows automate and visualize processes such as the student admission lifecycle.
Steps:
•	Navigate to Process Flow > New.
•	Provide details including name, label, and description.
•	Define stages such as New, InProgress, Joined, Rejected, Rejoined, Closed, and Cancelled.
•	Save and publish the process flow.
ORDER:Joined >> Rejected >> Rejoined >> Closed >> Cancelled

9. Client Scripts for Automation
Client Scripts automate actions and enforce form behavior.
Auto-Populate Admission Fields
Populates fields like Grade and Student Name when Admission Number is selected.
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   if (isLoading || newValue === '') return;
   var admission = g_form.getReference('u_admission_number');
   g_form.setValue('u_grade', admission.u_grade);
   g_form.setValue('u_student_name', admission.u_student_name);
}
Pincode-Based Field Update
Automatically fills Mandal, City, and District based on the entered Pincode.
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   if (isLoading || newValue === '') return;
   var pincode = g_form.getValue('u_pincode');
   if (pincode === '509358') {
      g_form.setValue('u_mandal', 'Kadthal');
      g_form.setValue('u_city', 'Kadthal');
      g_form.setValue('u_district', 'Ranga Reddy');
   }
}
Disable Fields for Student Progress
Prevents manual entry into specific fields on form load.
function onLoad() {
   g_form.setDisabled('u_total', true);
   g_form.setDisabled('u_percentage', true);
   g_form.setDisabled('u_result', true);
}
Total Marks Calculation
Calculates the total score from subject fields automatically.
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   var total = parseInt(g_form.getValue('u_telugu')) +
               parseInt(g_form.getValue('u_hindi')) +
               parseInt(g_form.getValue('u_english')) +
               parseInt(g_form.getValue('u_maths')) +
               parseInt(g_form.getValue('u_science')) +
               parseInt(g_form.getValue('u_social'));
   g_form.setValue('u_total', total);
}

10. Results
The implemented Educational Management System on ServiceNow provides:
•	Centralized management of student and admission data.
•	Automated workflows for consistent and error-free operations.
•	Dynamic forms and scripts that enhance data entry and validation.
•	Seamless tracking of student progress and admission stages.
Screenshots should be included for:
•	Table and form configurations
•	Process flow
•	Script execution in forms
 
11. Advantages
•	Accessible from any location with cloud support.
•	Automation reduces manual workload and increases accuracy.
•	Customizable for various educational institution needs.
•	Integrated system for admissions, student records, and performance.
•	Secure and role-based access control.

12. Disadvantages
•	Requires prior knowledge or training in ServiceNow for effective use.
•	Complex customization may be time-consuming.
•	Enterprise usage may involve licensing costs.

13. Future Scope
•	Integration with analytics tools like Tableau or Power BI for reporting.
•	Expansion to include teacher scheduling and performance tracking.
•	Mobile application support using ServiceNow Mobile Studio.
•	API-based connectivity with external systems and student databases.



