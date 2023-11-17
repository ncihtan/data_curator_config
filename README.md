# Project configurations for the [Data Curator App](github.com/sage-Bionetworks/data_curator)

The file [tenants.json](tenants.json) controls which DCCs appear in DCA. It contains a json object `tenants` which holds one json object per DCC. Each DCC object requires:\

-   `name`: The name of the DCC to appear in the DCA selection menu\
-   `synapse_asset_view`: The synapse ID of the DCCs fileview for DCA. Must include "syn"\
-   `config_location`: Filepath to the DCC's DCA config file. More details below.\

Each DCC will have its own directory to store configuration files. At minimum it will have [dca_config.json](demo/dca_config.json). This file can be validated against [schemas/dca_config.schema.json](schemas/dca_config.schema.json). At the top level it contains three json objects, `dcc`, `dca`, and `schematic`.\

`dcc` contains various configurations about your DCC and data model:\

-   `name` - name of DCC in dropdown menu
-   `synapse_asset_view` - synapse ID of asset view.
-   `data_model_url` - data model URL (**RAW** github file).
-   `data_model_info` - URL to a description of the data model, such as release notes. 
-   `template_menu_config_file` - URL to DCA template dropdown file.
-   `logo_location` - URL to logo file. 
-   `logo_link` - link to DCC website. 
-   `dcc_help_link` - link for users to find help about DCA. 
-   `portal_help_link` - link for users to find help about their portal. 

`dca` contains DCA-specific customizations:\

-   `use_compliance_dashboard` - `TRUE` or `FALSE`. Only FALSE currently supported. Data compliance dashboard.
-   `primary_col` - center header color hex code. 
-   `secondary_col` - right header color hex code. 
-   `sidebar_col` - left header color hex code. 

`schematic` contains several objects for passing parameters to schematic commands:\

-   `manifest_generate`

    -   `output_format`-`excel`or`google_sheets\`. [Schemtic manifest get ption](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-manifest-get).
    -   `use_annotations` - `TRUE` or `FALSE`. [Schemtic manifest get option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-manifest-get).

-   `model_validate`

    -   `restrict_rules` - `TRUE` or `FALSE`. [Schematic model validate and submit option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-model-validate).

-   `model_submit`

    -   `use_schema_labels` - `TRUE` or `FALSE`. [Schematic model submit option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-model-submit).
    -   `table_manipulation` - `replace` or `upsert`. [Schematic model submit option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-model-submit).
    -   `manifest_record_type` - One of `table_and_file`, `file_only` , `file_and_entities` or `table_file_and_entities`. [Schematic model submit option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-model-submit).
    -   `hide_blanks` - `TRUE` or `FALSE`. [Schematic model submit option](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-model-submit).

Each DCC also needs a template configuration file. This controls which data types are accessible to users and if they contain record-based or file-based data. It can be generated by hand or automatically from a data model using the [dca-template-config-action github action](https://github.com/Sage-Bionetworks/dca-template-config-action). See an [example workflow in a data model repo](https://github.com/Sage-Bionetworks/data-models/blob/main/.github/workflows/create-template-config.yml). This json file can be validated against [schemas/dca_template_config.schema.json](schemas/dca_template_config.schema.json). The top level of the file needs a json array of objects named `manifest_schemas`. Each object in the array requires the strings:

-   `display_name`: Display name of the data type
-   `schema_name`: Name of the schema
-   `type`: record or file

See our [example dca_template_config.json](https://github.com/Sage-Bionetworks/data-models/blob/main/dca-template-config.json)
