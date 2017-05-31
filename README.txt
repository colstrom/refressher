NAME
  refressher -- Review Tool for OpenSSH Configuration Files

SYNOPSIS
  refressher [ options ]

DESCRIPTION
  refressher is a tool for reviewing OpenSSH configuration files. It can identify undocumented settings (often unsupported historic settings), and
  cases where the value defined is equivalent to the current default for that setting. These can be extracted for review, or removed from generated
  output. Additionally, it provides a future-proof pretty printer by ingesting man pages at runtime and formatting according to the style used in
  the documentation. The resulting output is sorted (by default) to minimize diffs with configuration under version control. The intent of this
  tool is to reduce cognitive load when reviewing and modifying configuration.

OPTIONS
  -h              Display help text and exit.
  -V              Display version and exit.
  -f, --file=file Path to configuration file. Default depends on --type:
                    --type=server
                          The default value is /etc/ssh/sshd_config.
                    --type=client
                          The default value is ${HOME}/.ssh/config.
  -c, --comment=action
                  How to handle comments. The default value is drop.
  -d, --default=action
                  How to handle options set to default values. The default value is keep.
  -e, --empty=action
                  How to handle empty lines. The default value is drop.
  -n, --no-sort   Do not sort output. Useful when using refressher only for formatting. Ignores -d if set.
  -u, --unknown=action
                  How to handle unrecognized keywords. The default value is keep.
  -t, --type=type Type of configuration to process (client or server). The default value is server.
  --show-license-text
                  Display full license text and exit.

ACTIONS
  For each line of the configuration file, one of the following actions is applied:
    drop  Drop lines of this type (they will not appear in output).
    keep  Keep lines of this type (they will appear in output).
    show  Only show lines of this type. Expected output when this is set for multiple types is undefined.

ENVIRONMENT VARIABLES
  The default values can be altered to account for platform differences by using the following environment variables:
    SSHD_CONFIG
          The location of sshd_config. The default value is /etc/ssh/sshd_config.
    SSHD_CONFIG_MANUAL_PAGE
          The manual page for sshd_config. The default value is sshd_config.
    SSHD_CONFIG_MANUAL_SECTION
          The manual section where the page for sshd_config can be found. The default value is 5.
    SSH_CONFIG
          The location of ssh_config. The default value is ${HOME}/.ssh/config.
    SSH_CONFIG_MANUAL_PAGE
          The manual page for ssh_config. The default value is ssh_config.
    SSH_CONFIG_MANUAL_SECTION
          The manual section where the page for ssh_config can be found. The default value is 5.

EXIT STATUS
    0     Success
    1     Failure
    100   Error (Permanent)
    111   Error (Temporary)

SEE ALSO
   sshd_config(5), ssh_config(5)

IMPLEMENTATION
  version         1.0.0
  author          Chris Olstrom <chris@olstrom.com>
  copyright       Copyright (c) 2017 Chris Olstrom
  copyright       Copyright (c) 2017 SUSE LLC
  license         MIT (use --show-license-text for full text)
