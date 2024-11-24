# HLL_CRCON_All_time_stats

A plugin for Hell Let Loose (HLL) CRCON (see : https://github.com/MarechJ/hll_rcon_tool) that displays statistic data about the player asking for them in chat (`!me`) ;

![375490122-d8c7be50-aa6e-4949-b789-c327cacb2a1a](https://github.com/user-attachments/assets/4e9105d9-f87b-40e9-a489-da74cbb8f267)

## Install
- Log into your CRCON host machine using SSH and enter these commands :
  ```shell
  cd /root/hll_rcon_tool
  wget https://raw.githubusercontent.com/ElGuillermo/HLL_RCON_restart/refs/heads/main/restart.sh
  mkdir custom_tools
  cd custom_tools
  wget https://raw.githubusercontent.com/ElGuillermo/HLL_CRCON_All_time_stats/refs/heads/main/hll_rcon_tool/custom_tools/all_time_stats.py
  ```
- Edit `/root/hll_rcon_tool/rcon/hooks.py` and add these lines:
  - (in the import part, on top of the file)
    ```python
    import custom_tools.all_time_stats as all_time_stats
    ```
  - (at the very end of the file)
    ```python
    @on_chat
    def alltimestats(rcon: Rcon, struct_log: StructuredLogLineWithMetaData):
      all_time_stats.all_time_stats(rcon, struct_log)
    ```

## Config
- Edit `/root/hll_rcon_tool/custom_tools/all_time_stats.py` and set the parameters to your needs ;
- Restart CRCON :
  ```shell
  cd /root/hll_rcon_tool
  sh ./restart.sh
  ```

## Limitations
⚠️ Any change to these files requires a CRCON rebuild and restart (using the `restart.sh` script) to be taken in account :
- `/root/hll_rcon_tool/custom_tools/all_time_stats.py`
- `/root/hll_rcon_tool/rcon/hooks.py`

⚠️ This plugin requires a modification of the `/root/hll_rcon_tool/rcon/hooks.py` file, which originates from the official CRCON depot.  
If any CRCON upgrade implies updating this file, the usual upgrade procedure, as given in official CRCON instructions, will **FAIL**.  
To successfully upgrade your CRCON, you'll have to revert the changes back, then reinstall this plugin.  
To revert to the original file :  
```shell
cd /root/hll_rcon_tool
git restore rcon/hooks.py
```
