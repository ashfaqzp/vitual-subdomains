# vitual-subdomains
vitual-subdomains with htaccess

You need to add entries for subdomains in etc/hosts for local

127.0.0.1      moblink.testurl.test

127.0.0.1      ufone.testurl.test


#In laravel you have to do like this without htaccess changes

sub-domain for every user or company, like laraveldaily.slack.com. How to handle these subdomains in Laravel routes?

The code in routes/web.php is pretty straightforward:

'''
Route::domain('{company_name}.workspace.com')->group(function () {
    Route::get('users', 'UsersController@index');
	// Route::get('/', ['uses' => '\App\Http\Controllers\Front\HomeController@index'])->name('front.home');

});

// Route::get('/{slug?}', ['uses' => '\App\Http\Controllers\Front\HomeController@index'])->name('front.home');

'''

So {company_name} could be any value (of course, you need to configure it in your domain DNS records, too), and then this will come as a parameter variable to the Controller, with the same name.

'''
public function index($slug)
{
    $company = Company::findOrFail($slug);
    $users = User::where('company_id', $company->id)->get();
    return view('users.index', compact('users'));
}

'''
