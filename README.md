# MongoDB.OptionSerializer
MongoDB serializer for [nlkl/Optional](https://github.com/nlkl/Optional)

# Usage

    public class MyType
    {
        public Option<MyPropertyType> MyProperty { get; set; }
    }
    
To deserialize this class from the MongoDB BsonDocument you need to define how to map the option value by setting the OptionSerializer for the optional property.

    BsonClassMap.RegisterClassMap<MyType>(cm => {
                    cm.AutoMap();
                    cm.SetIgnoreExtraElements(true);
                    cm.MapMember(c => c.MyProperty)
                      .SetElementName("Bson_Property")
                      .SetSerializer(new OptionSerializer<MyPropertyType>());
                });
