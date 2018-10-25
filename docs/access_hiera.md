# Accessing Hiera Data on Puppet Master

## Requirements

Old version of puppet was used due to what was deployed in production

## Procedure

1. make sure that the Hiera utility is available
   ```
   hiera
   ```
   else install the Hiera utility, by running:
   ```
   gem install hiera hiera-puppet
   ```

2. locate the `puppet.conf` file location which provides the
   the location of the Hiera config file:
   ```
   find / -iname "puppet.conf"
   ```

   The path of the Hiera config file is located in the key:
   `hiera_config`

3. the Hiera config file provides, among other things, the order and list of the
   Hiera data files. The Hiera data files which are listed first takes precedence
   on the ones further down. In effect, if a variable is listed in 2 files, the
   variable in the first file will be the effective one.

4. To look up a variable in Hiera, do the following:
   ```
   hiera <variable_to_lookup> <facts_supplied> -c <hiera_config_file_path>
   ```
   where:
     1. `<variable_to_lookup>` is the variable to look up in the Hiera data files
     2. `<hiera_config_file_path>` is the path to the Hiera config file as described above
     3. `<facts_supplied>` are the facts that are normally supplied by Puppet itself and needs
        to supplied to the Hiera utility because Hiera reads the Hiera data only and does not
        interact with Puppet facter.
        The format `<facts_supplied>` is `::<factor_key>=<factor_value>`.

        [**untested**] it might be possible
        to repeat this `<facts_supplied>` in order to supply many facts.
