# Select Request - Built with Quasar Framework

## Install components in Quasar Framework
	* QTooltip
	* QSpinnerTail
	* QIcon
	* QSelect

## Required plugins
	* axios (https://www.npmjs.com/package/axios)

## Properties
	* label (required | String | Select label)
	* url (required | String | Url request)
	* configOptions (required | Object | Set label and value on return of request)
	* error (optional | Boolean | If set to true, the input field’s colors are changed to show there is an error)
	* params (optional | Object | Optional parameters for the request - Query String)
	* filter (optional | Boolean | Propertie native q-select - filter)
	* radio (optional | Boolean | Propertie native q-select - radio)
	* toggle (optional | Boolean | Propertie native q-select - toggle)
	* separator (optional | Boolean | Propertie native q-select - separator)

## Events emitted
	* error (optional | Handle error emitted)
