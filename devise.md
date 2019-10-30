
## verify a user's password in Devise

user = User.find_for_authentication(email: params[:user][:email])
user.valid_password?(params[:user][:password])

with strong params

def login
  user = User.find_for_authentication(email: login_params[:email])

  if user.valid_password?(login_params[:password])
    user.remember_me = login_params[:remember_me]
    sign_in_and_redirect(user, event: :authentication)
  end
end

private
def login_params
  params.require(:user).permit(:email, :password, :remember_me)
end

