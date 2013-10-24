User Agent Helper Functions
===========================

This set of helper functions is aimed for convenience in use the CodeIgniter's
User_agent library. Tested on CodeIgniter 2.1.4 and CodeIgniter 3.0-dev (October, 2013).

Intallation
-----------

Place the file user_agent_helper.php within your application/helpers folder.

A Quick Test
------------

```php
$this->load->helper('user_agent');
var_dump(user_agent());
```

A Usage Example for Makihng an Adaptive HTML Boilerplate
--------------------------------------------------------

```php
if (!function_exists('template_support_oldie')) {

    /**
     * This function decides whether additional assets within a html template
     * to be loaded for supporting older versions of Internet Explorer.
     * Create within your system the following configuration options:
     * $config['ie_min_supported_version'] = 6;         // 6, 7, 8, 9, 10, ...
     * $config['load_assets_by_ua_detection'] = true;   // or false
     * @autor Ivan Tcholakov, 2013.
     * @license The MIT License, http://opensource.org/licenses/MIT
     * @return boolean
     */
    function template_support_oldie() {

        $ie_min_supported = config_item('ie_min_supported_version');

        if ($ie_min_supported < 9) {

            if (config_item('load_assets_by_ua_detection')) {

                ci()->load->helper('user_agent');

                $browser = user_agent_ie();

                if ($browser['is_ie']) {

                    if ($browser['ie_version'] < 9 &&
                        $browser['ie_version'] >= $ie_min_supported) {

                        return true;
                    }

                    return false;
                }

                return false;
            }

            return true;
        }

        return false;
    }

}
```

Author: Ivan Tcholakov <ivantcholakov@gmail.com>, 2012-2013.  
License: The MIT License (MIT), http://opensource.org/licenses/MIT