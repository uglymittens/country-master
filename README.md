# Country Master #

<i>Author:</i> Victor Choy [victor.cui@vibin.it](mailto: victor.cui@vibin.it)

<i>Copyright</i> © 2015 www.vibin.it

## About Counter-Master ##

This is an Android library project which I built for myself, since I needed to create a login and registration form using phone numbers (uses Google's [libphonenumber](https://github.com/googlei18n/libphonenumber)).
An example of how I use my library for registration screen... It contain a country picker using a Spinner, containing flags and names of each country in the list. By default,
I set the country prefix number (e.g. "+1" for the US), according to the locale of the device (next to the country Spinner dropdown). Finally, I placed an EditText
next to the right of the country code to capture the regional number (phone number without prefix).

Example Usage (assuming this code lives in a Fragment):

	CountryMaster cm = CountryMaster.getInstance(context);
    ArrayList<Country> countries = cm.getCountries();
    String countryIsoCode = cm.getDefaultCountryIso();
    Country country = cm.getCountryByIso(countryIsoCode);

	Spinner spinner = (Spinner) getActivity().findViewById(R.id.spinner_countries);
	CountrySpinnerAdapter adapter = new CountrySpinnerAdapter(context, R.layout.item_spinner_countries, countries);
    spinner.setAdapter(adapter);
    
    TextView tvCountryPrefix = (TextView) getActivity().findViewById(R.id.tv_dialprefix);
    tvCountryPrefix.setText("+" + country.mDialPrefix);
    
Let's say the presses the Spinner dropdown and selects a different country:

	@Override
	public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
		CountryMaster cm = CountryMaster.getInstance(getActivity());
		Country country = cm.getCountryByPosition(position);
		TextView tvCountryPrefix = (TextView) getActivity().findViewById(R.id.tv_dialprefix);
    	tvCountryPrefix.setText("+" + country.mDialPrefix);
	}
	
Let's say the user wants to submit the registration data:

	public void onClick(View view) {
		
		PhoneNumberUtil util = PhoneNumberUtil.getInstance();
		
		// assuming you only a button in your layout...
		boolean isAuthentic = false;
		try {
			PhoneNumber number = util.parse(mDialPrefix + mPhoneNumber, mCountryIso);
			isAuthentic = true;
		} catch (NumberParseException e) {
			e.printStackTrace();
		}
		if (isAuthentic) {
			// submit code or whatever
		}
	}


## About Vibin ##

We at Vibin make cool stuff... check out our Photo Notes app and give us feedback on what you think! It's a great way to organize your photos and tag them at the same time!

[App Store](https://itunes.apple.com/us/app/vibin-photo-notes/id749920897?mt=8), 
[Google Play](https://play.google.com/store/apps/details?id=it.vibin.app)

## Setting up ##

* Add this library as a dependency: Project -> Properties -> Android -> Add
* You will find a sample layout that you can use to get you going.
* I recommend using a Spinner and SpinnerAdapter to implement your drop-down (just a suggestion!)

If you need help, shoot me an email.

## Keywords ##

Keywords: android, library, libphonenumber, country, country code, phone number, iso code, validate, validation, login, registration

### Open Source Licenses ###

* [libphonenumber](https://github.com/googlei18n/libphonenumber)
 Copyright © 2009 Google
 Apache License Version 2.0, January 2004
 (Thanks guys!)
