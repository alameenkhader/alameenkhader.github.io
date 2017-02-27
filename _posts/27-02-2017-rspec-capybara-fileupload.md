---
layout: post
title:  "RSPEC: FILE UPLOAD"
date:   27-02-2017 02:44:26 +0530
categories: rails
---

1. Stack: Capybara, FactoryGirl

```
# spec/factories/document.rb
FactoryGirl.define do
  factory :document do
    attachment_type do
      Rack::Test::UploadedFile.new(Rails.root.join('spec', 'support', 'files', 'img.png'))
    end
  end
end
```

```
# spec/features/document_spec.rb
require 'rails_helper'

feature 'Profile - Documents', js: true do
  let!(:user) { create(:user) }
  let(:document) { build(:document) }

  before { login_as(user, scope: :user) }

  it 'uploads a valid document' do
    visit(edit_user_registration_path)
    select(document.attachment_type, from: 'attachment_type')
    attach_file('file-attach-field', document.attachment.path)
    find('#upload-doc-btn').click
    expect(page).to have_content('Successfully uploaded')
    within('.uploaded') do
        expect(page).to have_content(document.attachment_type)
    end
  end
end
```
