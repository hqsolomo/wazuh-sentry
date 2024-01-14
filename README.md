# wazuh-sentry

Tool for managing active response commands for Wazuh

Feel free to use it

## How It Works

Run `sudo sentry config --init` for first-time setup. This will take the following actions against `/var/ossec/etc/ossec.conf`:

  1. `sudo cp /var/ossec/etc/ossec.conf sentry/backup/manager-config/config-init_${TIMESTAMP}_ossec.conf`
  2. Search for comment `<!-- Active response -->`
  3. Insert comment `<!-- ${sentry-commands.conf} -->` to the line below
  4. Search for comment

    ```xml
    <!--<active-response>active-response options here</active-response>-->
    ```
    
  4. Removes wrapped comment tag from `<active-response>` element and wraps `active-response options here` in comment tag if they are present
  5. Search for tag `<active-response>`
  6. Insert comment `<!-- ${sentry-responses.conf} -->` to the line above `<active-response>`
  8. Writes existing `<command>` and `<active-response>` elements to `sentry-commands.conf` and `<sentry-responses.conf>`
  9. 

As `init` is _not_ idemptent it is highly recommended to keep backups of your ossec.conf file.

If your Wazuh manager config is not at that location, use `--manager-config /path/to/ossec.conf`. Wrap the path in quotes if it contains spaces. Alternatively, you can perform the above steps manually, using the path to your config instead of the default.

If you do not wish to enable active response management when using `init`, use the `--active-response skip` flag. This will skip steps 3 through 4 above. To disable active response management, use `--active-response disable`. To enable active response management, use `--active-response enable`. To enable active response management of the out-of-the-box active responses, use `--manage-default-responses yes`. To disable management of the out-of-the-box responses, use `--manage-default-responses no`. These flags are indempotent.
