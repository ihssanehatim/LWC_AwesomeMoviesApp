# Salesforce DX Project: Next Steps

Now that you’ve created a Salesforce DX project, what’s next? Here are some documentation resources to get you started.

## How Do You Plan to Deploy Your Changes?

Do you want to deploy a set of changes, or create a self-contained application? Choose a [development model](https://developer.salesforce.com/tools/vscode/en/user-guide/development-models).

## Configure Your Salesforce DX Project

The `sfdx-project.json` file contains useful configuration information for your project. See [Salesforce DX Project Configuration](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ws_config.htm) in the _Salesforce DX Developer Guide_ for details about this file.

## Read All About It

- [Salesforce Extensions Documentation](https://developer.salesforce.com/tools/vscode/)
- [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [Salesforce CLI Command Reference](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference.htm)
--------
## Requirements of this project

The main idea is to implement an app managing movies catalog,

### Data model ----

* *Movie__c*: 
    * Name 
        * Type: Text (250)
        * Required
    * Category (Picklist)
        * Required
        * Values:
            * Horror
            * Adventure
            * Action
            * Drama
            * Comedy
    * Description 
        * Type: text area (250)
    * Release date 
        * Type: Date
        * Required
    * FemaleActorsPercentage 
        * Type: Percent (with a comma)
    * MaleActorsPercentage
        * Type: Percent (with a comma)
    * IsReleased 
        * Type: Checkbox
* *Actor__c*:
    * Name
        * Type: Text (250)
    * Gender 
        * Type: checkboxsfc
    * Number of movies
        * Type: Number

* *MovieActor__c*
    * Junction object: Actor <=> Movie : (Many to Many)


### LWC -----

The app should contain three components communicating between each other:

* FilterMoviesLwc: 
    * The main purpose is to filter the movies shown in movies results section
    * Create new movie button (to open NewMovieModalLWC) 
* MoviesResultsLwc
    * Showing the results of the search
    * Using a grid
    * Each element is a tile (Image + Name + Category + Release Date)
* MoviePreviewLwc
    * Showing preview of a selected Movie ( Image, Name, Category, Release date)
    * Edit button to change the component to edit mode 
    * Delete movie
* NewMovieModalLWC
    * Show the component in a popup ( after clicking on create Movie button)
    * Custom fields to create a new movie
    * Custom lookup to search for actors and add them to the movie

### Automation: --------

* *Trigger*: 
    * Update number of movies in each related actor
    * Calculate gender percentage for Male and Female
* *Batch + Scheduler**:* 
    * Process all movies in the database to update isReleased field based on release date 

### Code guidelines: ------

* Keep the use of custom css to the minimum: use of SLDS classes (slds-grid, slds-col, slds-m-top_large, slds-size_1-of-2...) and keep responsiveness
* Prioritize the use of wire in LWC 
* Respect best practices