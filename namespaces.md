# Namespaces

## Global or Package Qualifier

The global or package qualifier was originally going to be simply "`::`" with no dot after it. However, it seemed like this qualifier might be very useful for doing things like referring to methods as members and universal function call syntax. Since global and package qualified names are likely to be very rare, it made sense to give them a longer syntax. However, no other symbol seemed to make sense for them. The additional dot was therefore introduced to distinguish them from any possible future use. The "`::.`" syntax seems to make sense because it is as if the global, unnamed namespace appears between the "`::`" and the "`.`". Perhaps that means that they should be separate operators so that "`:: .`" would be a valid qualifier.
