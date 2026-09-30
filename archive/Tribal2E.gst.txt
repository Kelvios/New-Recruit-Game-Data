<?xml version="1.0" encoding="utf-8"?>
<gameSystem xmlns="http://www.battlescribe.net/schema/gameSystemSchema" id="sys-e140-121e-9b34-0be3" name="TRIBAL 2nd Edition" revision="2" battleScribeVersion="2.03" authorName="TRIBAL 2nd Edition rules by Mana Press. NR data authored privately for personal use." type="gameSystem">
  <costTypes>
    <costType id="2583-462d-9a3d-8b99" name="Honour" defaultValue="0"/>
  </costTypes>
  <profileTypes>
    <profileType id="49d0-84ee-492f-492f" name="Unit">
      <characteristicTypes>
        <characteristicType id="aea1-39b1-ec9b-475a" name="Wounds"/>
        <characteristicType id="1200-2470-7a16-e426" name="Skills"/>
        <characteristicType id="fb14-0b46-30b6-76a9" name="Notes"/>
      </characteristicTypes>
    </profileType>
  </profileTypes>
  <categoryEntries>
    <categoryEntry id="21fb-7998-9dc4-5fd0" name="Warlord" hidden="false"/>
    <categoryEntry id="cdf2-4f60-5c31-a783" name="Heroes" hidden="false"/>
    <categoryEntry id="a20b-aa4e-9045-9c20" name="Warriors" hidden="false"/>
    <categoryEntry id="ef8f-b97c-ea97-503e" name="Marksmen" hidden="false"/>
    <categoryEntry id="cd73-16c4-bac1-dd3f" name="Shaman (optional rule)" hidden="false"/>
    <categoryEntry id="98ce-fd5f-59ba-0e1a" name="Historical Rules" hidden="false"/>
    </categoryEntries>
  <forceEntries>
    <forceEntry id="1128-7928-73f4-74fc" name="Warband" hidden="false">
      <categoryLinks>
        <categoryLink id="6b4a-25c7-3e18-ccad" name="Warlord" hidden="false" targetId="21fb-7998-9dc4-5fd0" type="category">
          <constraints>
            <constraint type="min" value="1" field="selections" scope="parent" shared="true" id="4715-e63e-6393-f0f0"/>
            <constraint type="max" value="1" field="selections" scope="parent" shared="true" id="19c3-d0a3-3f1b-bb6c"/>
          </constraints>
        </categoryLink>
        <categoryLink id="a62c-e2b5-4b3a-bbf8" name="Heroes" hidden="false" targetId="cdf2-4f60-5c31-a783" type="category">
          <constraints>
            <constraint type="min" value="0" field="selections" scope="parent" shared="true" id="fa53-eb38-a981-13d8"/>
            <constraint type="max" value="20" field="selections" scope="parent" shared="true" id="8864-7aeb-906c-22ef"/>
          </constraints>
        </categoryLink>
        <categoryLink id="16c8-fa15-1885-674b" name="Warriors" hidden="false" targetId="a20b-aa4e-9045-9c20" type="category">
          <constraints>
            <constraint type="min" value="0" field="selections" scope="parent" shared="true" id="aab6-efe0-e3ff-cd0a"/>
          </constraints>
        </categoryLink>
        <categoryLink id="97c0-7e4a-3adc-ee75" name="Marksmen" hidden="false" targetId="ef8f-b97c-ea97-503e" type="category">
          <constraints>
            <constraint type="min" value="0" field="selections" scope="parent" shared="true" id="e3c5-1f14-ded4-494b"/>
            <constraint type="max" value="2" field="selections" scope="parent" shared="true" id="07c1-1442-e8ed-afdc"/>
          </constraints>
        </categoryLink>
        <categoryLink id="9b80-89d0-5dac-16dc" name="Shaman (optional rule)" hidden="false" targetId="cd73-16c4-bac1-dd3f" type="category">
          <constraints>
            <constraint type="min" value="0" field="selections" scope="parent" shared="true" id="f389-7ca1-389d-185f"/>
            <constraint type="max" value="1" field="selections" scope="parent" shared="true" id="d0d5-3047-0616-9f3c"/>
          </constraints>
        </categoryLink>
        <categoryLink id="7949-5fa3-abf7-d41a" name="Historical Rules" hidden="false" targetId="98ce-fd5f-59ba-0e1a" type="category">
          <constraints>
            <constraint type="min" value="0" field="selections" scope="parent" shared="true" id="125e-4b20-9787-4c94"/>
          </constraints>
        </categoryLink>
      </categoryLinks>
    </forceEntry>
  </forceEntries>
</gameSystem>
