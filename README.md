# LTI Memberships services for Moodle

This repository contains an implementation of the following 1EdTech Learning Tools Interoperability (LTI) services:
* [Membership](https://www.imsglobal.org/specs/ltimemv1p0)
* [Names and Role Provisioning (NRPS)](https://www.imsglobal.org/spec/lti-nrps/v2p0)
* [Course Groups](https://www.imsglobal.org/spec/lti-gs/v1p0)

It enhances the existing Memberships service available in Moodle core as follows:
* includes the username property in the NRPS response
* includes the Course Groups service (Candidate Final, issued 1 October 2019)

Moodle versions 3.9 or later are supported so there is no need to upgrade to the latest release of Moodle to take advantage of newly supported services.

## Installation

Moodle implements all LTI services as sub-plugins (of type ltiservice).  So this implementation can be installed (and managed) in the same way as any other Moodle plugin:

1. Log into Moodle as a site administrator
1. Navigate to the *Site Administration* area
1. Select the *Plugins* tab
1. Click on the *Install plugins* link
1. Click on the *Install plugins from the Moodle plugins directory* button
1. Select *External tool / LTI service* as the plugin type
1. Select the *LTI Memberships* service plugin
1. Click on the *Install now* button

The service can also be installed manually by downloading the source code from the Moodle plugins directory or from the [GitHub repository](https://github.com/celtic-project/moodle-ltiservice_memberships_celtic).

## Implementation notes

This implementation extends the Moodle implementation of the official LTI services in the following ways.

### Membership service

* The roles array for each member will include the fully-qualified name of any roles specified using their short name (in addition tp the short name)
* A Moodle-specific role is added for each Moodle role associated with the member; e.g. https://moodle.org/lti/user/role/editingteacher or https://moodle.org/lti/user/role/student

### Names and Role Provisioning services

* The response includes a member's username in a property named `ext_user_username` (to be consistent with the response from the *Membership* service)
* The roles array for each member will include the fully-qualified name of any roles specified using their short name (in addition tp the short name)
* A Moodle-specific role is added for each Moodle role associated with the member; e.g. https://moodle.org/lti/user/role/editingteacher or https://moodle.org/lti/user/role/student

### Context Groups service

* A `set_ids` property is included in the response to provide support for groups which belong to more than one set (grouping).  The property is an array of strings with an entry for each set to which the group belongs.  The value of each entry is the ID of the set.  The `set_id` property is also included in the response for those groups which belong to a single set, but is omitted when a group does not belong to a set or belongs to more than one set.

## Feedback/issues

Please report any feedback or issues with this code via the [Issues area](https://github.com/celtic-project/moodle-ltiservice_memberships_celtic/issues) of the GitHub repository.
