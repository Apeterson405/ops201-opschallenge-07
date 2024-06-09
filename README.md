# ops201-opschallenge-07


#!/bin/bash

# Check if running as root
if [ "$(id -u)" != "0" ]; then
    echo "This script must be run as root" 1>&2
    exit 1
fi

# Function to display component information
display_component_info() {
    component_name="$1"
    grep -E "$component_name|description|product|vendor|physical id|bus info|width|clock|capabilities|configuration|resources|logical name|version|serial|size|capacity" | sed 's/^[ \t]*//' | sed 's/^[ \t]*//' | sed '/^$/d' | sed '/^\*/d'
}

# Display system information
echo "Name of the computer:"
lshw -C system | display_component_info "system"
echo

echo "CPU:"
lshw -C cpu | display_component_info "processor"
echo

echo "RAM:"
lshw -C memory | display_component_info "memory"
echo

echo "Display adapter:"
lshw -C display | display_component_info "display"
echo

echo "Network adapter:"
lshw -C network | display_component_info "network"

end
