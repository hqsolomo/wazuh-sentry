# wazuh-sentry

Tool for managing active response commands for Wazuh

Feel free to use it

## How It Works

Run `sudo sentry --init` for first-time setup. This will do the following:

  * Search for comment `<!-- Active response -->` in `/var/ossec/etc/ossec.conf`
  * Insert comment `<!-- Sentry commands><-->` to the line below
  * Searh for comment
    ```xml
    <!--
  <active-response>
    active-response options here
  </active-response>
  -->
    ```
  * Search for tag <active-response> (even if it is commented out)
  * Insert comment `<!-- Sentry responses><-->` to the line below

If your Wazuh manager config is not at that location, use `--init-file /path/to/ossec.conf`. Wrap the path in quotes if it contains spaces. Alternatively, you can perform the above steps manually, using the path to your config instead of the default.
